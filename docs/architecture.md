# Arquitectura Técnica
# ChillTechControl

**Versión:** 1.0  
**Fecha:** Mayo 2026

---

## 1. Visión general de la arquitectura

ChillTechControl sigue una arquitectura de **microservicios** con una separación clara entre el agente nativo que corre en el dispositivo del hijo y los servicios en la nube que coordinan la lógica de negocio.

> **Alcance MVP:** el agente del hijo es Android-only. La app del padre es multiplataforma (iOS + Android). El dashboard web y el agente iOS quedan para V1.1+.

```
┌─────────────────────────────────────────────────────────────────────┐
│                         DISPOSITIVOS                                │
│                                                                     │
│  ┌──────────────────┐          ┌──────────────────────────────┐     │
│  │  App Padre       │          │  Agente Hijo (nativo)        │     │
│  │  (React Native)  │          │  Android: Kotlin              │     │
│  │  iOS / Android   │          │                               │     │
│  └────────┬─────────┘          └──────────────┬───────────────┘     │
└───────────┼──────────────────────────────────┼────────────────────┘
            │ HTTPS/REST + WebSocket            │ HTTPS/REST
            ▼                                   ▼
┌─────────────────────────────────────────────────────────────────────┐
│                         API GATEWAY                                 │
│                    (NestJS + TypeScript)                             │
│                    Auth · Rate Limiting · Routing                    │
└────┬─────────────────┬──────────────────┬───────────────┬───────────┘
     │                 │                  │               │
     ▼                 ▼                  ▼               ▼
┌─────────┐    ┌──────────────┐   ┌─────────────┐  ┌──────────────┐
│ Auth    │    │ Family       │   │ Monitoring  │  │ Notification │
│ Service │    │ Service      │   │ Service     │  │ Service      │
└────┬────┘    └──────┬───────┘   └──────┬──────┘  └──────┬───────┘
     │                │                  │                │
     ▼                ▼                  ▼                ▼
┌─────────────────────────────────────────────────────────────────────┐
│                         CAPA DE DATOS                               │
│                                                                     │
│  ┌────────────────┐   ┌───────────────┐   ┌──────────────────────┐ │
│  │  PostgreSQL    │   │  Redis        │   │  Firebase Cloud      │ │
│  │  (datos        │   │  (sesiones,   │   │  Messaging           │ │
│  │   persistentes)│   │   caché,      │   │  (notificaciones)    │ │
│  │                │   │   tiempo real)│   │                      │ │
│  └────────────────┘   └───────────────┘   └──────────────────────┘ │
└─────────────────────────────────────────────────────────────────────┘
```

---

## 2. Componentes del sistema

### 2.1 App Padre (React Native)

La aplicación móvil usada por el padre/madre para gestionar los perfiles de sus hijos.

| Aspecto | Decisión |
|---|---|
| Framework | React Native (cross-platform iOS/Android) |
| Gestión de estado | Zustand |
| Navegación | React Navigation v6 |
| UI Library | React Native Paper (Material Design 3) |
| Cliente HTTP | Axios con interceptores de autenticación |
| Tiempo real | Socket.IO client (para actualizaciones live del tiempo de uso) |
| Almacenamiento local | Async Storage (tokens, preferencias) |

**Módulos principales (MVP):**
- `auth/` — Login, registro, recuperación de contraseña
- `family/` — Gestión de perfiles de hijos
- `rules/` — Configuración de límites y horarios
- `dashboard/` — Panel de monitoreo en tiempo real
- `requests/` — Gestión de solicitudes de tiempo extra

**Módulos planificados para V1.1+:** `reports/` (reportes semanales), `rewards/` (actividades recompensadas).

---

### 2.2 Agente de Monitoreo (Dispositivo del Hijo)

Aplicación nativa Android instalada en el dispositivo del hijo. Es el componente más crítico del sistema.

#### Android (Kotlin) — MVP

Usa las siguientes APIs del sistema:

| API | Uso |
|---|---|
| `UsageStatsManager` | Medir tiempo de uso activo de pantalla |
| `DevicePolicyManager` | Bloqueo del dispositivo al agotar el tiempo |
| `AccessibilityService` | Detectar apps en primer plano |
| `ForegroundService` | Monitoreo continuo en segundo plano |
| `BroadcastReceiver` | Detectar encendido del dispositivo para reiniciar el servicio |
| `Room` (SQLite) | Cache local de reglas y buffer de uso para modo offline |

#### iOS (Swift) — V1.1+

Fuera del alcance del MVP. El soporte iOS requiere las APIs `FamilyControls`, `ManagedSettings`, `DeviceActivity` y `AuthorizationCenter`, sujetas al entitlement `Family Controls` que Apple sólo otorga bajo solicitud.

**Funcionamiento offline:**

El agente cachea localmente las reglas de tiempo y el horario de descanso. Si pierde conexión con el backend:
- Sigue aplicando los límites y bloqueos según las últimas reglas conocidas (fail-open: no bloquea por desconexión).
- Acumula el uso en un buffer local.
- Al reconectar, sincroniza el uso pendiente y descarga reglas actualizadas.

**Flujo del agente:**
```
Inicio del dispositivo
        │
        ▼
   Iniciar servicio en background
        │
        ▼
   ¿Tiempo disponible hoy?
        │
   ┌────┴────┐
  No         Sí
   │          │
   ▼          ▼
Activar    Monitorear uso activo
Modo Chill      │
                ▼
         Cada 30 segundos:
         registrar tiempo usado
                │
                ▼
         Sincronizar con backend
         (cada 5 min o en cambio)
                │
                ▼
         ¿Queda < 15 min?
                │
         ┌──────┴──────┐
        No             Sí
                        │
                        ▼
                  Enviar aviso
                  al niño
```

---

### 2.3 API Gateway (NestJS + TypeScript)

Punto de entrada único para todos los clientes. Responsable de:
- Autenticación JWT
- Autorización por rol (padre / hijo / dispositivo-agente)
- Rate limiting (100 req/min por usuario)
- Routing a microservicios internos
- Logging centralizado

**Endpoints principales:**

```
POST   /auth/register
POST   /auth/login
POST   /auth/refresh

GET    /families/:id
POST   /families
POST   /families/:id/children
GET    /families/:id/children

GET    /children/:id/rules
PUT    /children/:id/rules
GET    /children/:id/usage/today
GET    /children/:id/usage/week

POST   /devices/heartbeat          ← agente reporta tiempo usado
POST   /devices/link               ← vincular dispositivo

POST   /requests                   ← niño solicita tiempo extra
GET    /requests/:parentId/pending
PUT    /requests/:id               ← padre aprueba/rechaza

GET    /reports/:childId/weekly
```

---

### 2.4 Servicios internos

#### Auth Service
- Registro, login, refresh tokens
- JWT con expiración de 15 min (access) + 30 días (refresh)
- Almacenamiento de refresh tokens en Redis con TTL

#### Family Service
- CRUD de familias, hijos y reglas
- Cálculo del tiempo permitido para el día actual según reglas configuradas
- Gestión de solicitudes de tiempo extra

#### Monitoring Service
- Recibe heartbeats del agente cada 5 minutos
- Calcula el tiempo restante
- Publica eventos en Redis Pub/Sub cuando el tiempo cambia (para WebSocket al padre)
- Detecta anomalías (agente que no reporta por más de 1 hora)

#### Notification Service
- Consume eventos del Monitoring Service
- Envía notificaciones push vía Firebase Cloud Messaging
- Gestiona templates de notificaciones según el evento y el idioma
- Respeta las preferencias de notificación del usuario

---

### 2.5 Dashboard Web — V1.1+

Fuera del alcance del MVP. Toda la gestión del padre se hace desde la app móvil React Native. Stack tentativo cuando se construya: React 18 + TypeScript + Vite + Tailwind + shadcn/ui + Recharts.

---

## 3. Modelo de datos

### Entidades principales (MVP)

```sql
-- Usuarios (padres)
CREATE TABLE users (
    id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    email       VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255),          -- NULL si usa OAuth
    name        VARCHAR(100) NOT NULL,
    avatar_url  VARCHAR(500),
    plan        VARCHAR(20) DEFAULT 'free',  -- 'free' | 'family'
    created_at  TIMESTAMPTZ DEFAULT NOW(),
    updated_at  TIMESTAMPTZ DEFAULT NOW()
);

-- Familias (en MVP, una familia tiene un solo owner_id; co-administradores en V1.1)
CREATE TABLE families (
    id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name        VARCHAR(100),
    owner_id    UUID REFERENCES users(id),
    created_at  TIMESTAMPTZ DEFAULT NOW()
);

-- Perfiles de hijos
CREATE TABLE children (
    id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    family_id   UUID REFERENCES families(id),
    name        VARCHAR(100) NOT NULL,
    age         INT,
    avatar_url  VARCHAR(500),
    pin_hash    VARCHAR(255),    -- para acciones en el dispositivo
    created_at  TIMESTAMPTZ DEFAULT NOW()
);

-- Dispositivos vinculados
CREATE TABLE devices (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    child_id        UUID REFERENCES children(id),
    device_token    VARCHAR(500) UNIQUE NOT NULL,  -- token del agente
    platform        VARCHAR(10) NOT NULL,           -- 'android' | 'ios'
    device_name     VARCHAR(100),
    last_heartbeat  TIMESTAMPTZ,
    created_at      TIMESTAMPTZ DEFAULT NOW()
);

-- Reglas de tiempo (por hijo)
CREATE TABLE time_rules (
    id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    child_id    UUID REFERENCES children(id),
    day_of_week INT,            -- 0=Dom, 1=Lun, ..., 6=Sáb. NULL = todos los días
    daily_limit_minutes INT NOT NULL,
    created_at  TIMESTAMPTZ DEFAULT NOW(),
    updated_at  TIMESTAMPTZ DEFAULT NOW()
);

-- Horarios de descanso (franjas sin pantallas)
CREATE TABLE quiet_hours (
    id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    child_id    UUID REFERENCES children(id),
    day_of_week INT,            -- NULL = todos los días
    start_time  TIME NOT NULL,
    end_time    TIME NOT NULL,
    is_active   BOOLEAN DEFAULT TRUE,
    created_at  TIMESTAMPTZ DEFAULT NOW()
);

-- Registro de uso diario
CREATE TABLE usage_logs (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    device_id       UUID REFERENCES devices(id),
    date            DATE NOT NULL,
    total_minutes   INT DEFAULT 0,
    last_updated    TIMESTAMPTZ DEFAULT NOW(),
    UNIQUE (device_id, date)
);

-- Sesiones de uso (para granularidad de reportes)
CREATE TABLE usage_sessions (
    id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    device_id   UUID REFERENCES devices(id),
    started_at  TIMESTAMPTZ NOT NULL,
    ended_at    TIMESTAMPTZ,
    duration_minutes INT
);

-- Solicitudes de tiempo extra
CREATE TABLE time_requests (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    child_id        UUID REFERENCES children(id),
    message         TEXT,
    status          VARCHAR(20) DEFAULT 'pending',  -- 'pending'|'approved'|'rejected'
    requested_at    TIMESTAMPTZ DEFAULT NOW(),
    responded_at    TIMESTAMPTZ,
    granted_minutes INT,                 -- minutos concedidos si se aprueba
    parent_note     TEXT                 -- mensaje del padre al rechazar
);
```

### Entidades planificadas para V1.1+

Las siguientes tablas no se crean en el MVP. Se diseñarán e introducirán cuando llegue su funcionalidad:

- `family_members` — co-administradores de la familia.
- `reward_activities` — actividades configurables que dan tiempo extra al niño.
- `reward_completions` — registro de actividades completadas y verificadas.

---

## 4. Seguridad

### 4.1 Autenticación y autorización

- **JWT con doble token:** Access token (15 min) + Refresh token (30 días, almacenado en Redis)
- **Roles MVP:** `parent`, `device-agent` (token diferente para el agente). El rol `co-parent` se introduce en V1.1.
- **Autorización basada en recursos:** Un padre solo puede acceder a los hijos de su familia
- El agente tiene un token de dispositivo de larga duración pero con permisos limitados (solo reportar uso y leer reglas)

### 4.2 Protección de datos del niño

- No se graba contenido de pantalla, capturas, ni historial de apps individuales en MVP
- Solo se almacena: tiempo de uso total por día y sesiones de uso (start/end)
- Datos encriptados en reposo (PostgreSQL con encriptación a nivel de columna para datos sensibles)
- Cumplimiento con **COPPA** (Children's Online Privacy Protection Act) y **GDPR**

### 4.3 Protección del agente

- El agente no puede ser desinstalado sin el PIN del padre (DevicePolicyManager en Android)
- Comunicación agente ↔ backend por HTTPS con certificate pinning
- El token del agente se rota cada 90 días

### 4.4 Seguridad en la API

- Rate limiting: 100 req/min por usuario autenticado, 20 req/min para endpoints públicos
- Validación de input con `class-validator` en todos los DTOs
- Protección contra IDOR: todas las queries filtran por `family_id` del usuario autenticado
- OWASP Top 10 como checklist para el security review de cada release

---

## 5. Infraestructura y despliegue

```
GitHub Repository
      │
      ▼
GitHub Actions CI/CD
      │
   ┌──┴──┐
  Test  Build
   │      │
   └──┬───┘
      ▼
  Docker Image
      │
      ▼
  AWS ECS (Fargate)   ←── Auto Scaling
      │
  ┌───┴───────────────────┐
  │   Load Balancer       │
  │   (Application LB)    │
  └───┬───────────────────┘
      │
  ┌───┴──────┬────────────┐
  │          │            │
  ▼          ▼            ▼
API       Monitoring   Notification
Service   Service      Service
  │          │
  ▼          ▼
RDS          ElastiCache
(PostgreSQL) (Redis)
```

### Entornos

| Entorno | Descripción | URL |
|---|---|---|
| `development` | Local con Docker Compose | localhost |
| `staging` | Replica de producción con datos de prueba | staging.chilltechcontrol.app |
| `production` | Entorno real | api.chilltechcontrol.app |

---

## 6. Decisiones de arquitectura (ADRs)

### ADR-001: React Native para la app de padres
**Decisión:** Usar React Native en lugar de apps nativas separadas.  
**Razón:** El equipo tiene más experiencia en JavaScript/TypeScript. El rendimiento es aceptable para una app de configuración y monitoreo (no un juego). Reduce el tiempo de desarrollo a la mitad.  
**Consecuencia:** Algunas funcionalidades del agente requieren módulos nativos custom, pero la app de padres puede ser 100% JS.

### ADR-002: Agentes nativos en Kotlin/Swift
**Decisión:** El agente en el dispositivo del hijo es nativo, NO una app React Native.  
**Razón:** El monitoreo en background, el acceso a `UsageStatsManager` y el bloqueo del dispositivo requieren APIs del sistema que no están accesibles desde React Native sin módulos nativos complejos. La app nativa es más confiable y consume menos batería.

### ADR-003: NestJS para el backend
**Decisión:** NestJS sobre Express puro o Fastify.  
**Razón:** NestJS provee estructura (módulos, decoradores, DI), facilita la separación en microservicios y tiene soporte nativo para WebSockets, validación y autenticación.

### ADR-004: Redis para tiempo real
**Decisión:** Usar Redis Pub/Sub para comunicar el Monitoring Service con el WebSocket Gateway.  
**Razón:** Permite escalar horizontalmente el API Gateway mientras mantiene la capacidad de entregar actualizaciones en tiempo real al padre. Cada instancia del gateway se suscribe a los eventos relevantes.
