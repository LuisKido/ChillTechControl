# Product Requirements Document (PRD)
# ChillTechControl

**Versión:** 1.0  
**Fecha:** Mayo 2026  
**Estado:** Borrador

---

## 1. Resumen ejecutivo

ChillTechControl es una aplicación de gestión del tiempo de pantalla diseñada para familias con hijos de entre 4 y 16 años. A diferencia de las soluciones actuales que se centran únicamente en el control parental restrictivo, ChillTechControl adopta un enfoque **colaborativo y educativo**: padres e hijos gestionan juntos el uso tecnológico, fomentando el autocontrol, la negociación y el desarrollo de hábitos digitales saludables.

---

## 2. Problema que resolvemos

### 2.1 Contexto

- El 75% de los niños entre 5 y 14 años usa dispositivos digitales más de 3 horas al día (fuente: OMS, 2024).
- El exceso de tiempo de pantalla se asocia con: trastornos del sueño, dificultades de concentración, sobrepeso infantil y menor desarrollo de habilidades sociales.
- Las herramientas actuales de control parental son percibidas por los niños como **represivas**, generando conflictos familiares.

### 2.2 Dolor del usuario

| Rol | Problema |
|---|---|
| Padre/Madre | No sé cuánto tiempo pasan mis hijos en el teléfono ni en qué apps |
| Padre/Madre | Cada vez que les quito el dispositivo hay una pelea |
| Padre/Madre | Las herramientas actuales son demasiado técnicas o complejas |
| Hijo/a | Me quitan el teléfono sin aviso y sin explicación |
| Hijo/a | Siento que no confían en mí |
| Hijo/a | No sé cuánto tiempo me queda disponible |

---

## 3. Objetivos del producto

### 3.1 Objetivos primarios

- **OBJ-01:** Permitir a los padres configurar límites de tiempo de pantalla en menos de 5 minutos.
- **OBJ-02:** Reducir los conflictos relacionados con el uso de pantallas en el hogar.
- **OBJ-03:** Dar a los niños visibilidad en tiempo real de su tiempo disponible.
- **OBJ-04:** Promover actividades offline mediante el Modo Chill.

### 3.2 Objetivos secundarios

- **OBJ-05:** Generar reportes semanales que los padres puedan revisar en menos de 2 minutos.
- **OBJ-06:** Permitir que el niño gane autonomía progresiva a medida que demuestra autocontrol.

---

## 4. Métricas de éxito (KPIs)

| Métrica | Meta a 6 meses | Meta a 12 meses |
|---|---|---|
| Familias activas (MAU) | 10,000 | 50,000 |
| Tasa de retención a 30 días | > 60% | > 70% |
| NPS (Net Promoter Score) | > 40 | > 55 |
| Conflictos reportados reducidos (encuesta) | - 30% vs. baseline | - 50% vs. baseline |
| Sesiones de "Modo Chill" completadas por día | 2 por familia | 3 por familia |
| Tiempo promedio de configuración inicial | < 5 min | < 3 min |

---

## 5. Usuarios objetivo

### 5.1 Personas

#### Persona 1 — "La Mamá Consciente"
- **Nombre:** Laura, 38 años
- **Ocupación:** Profesora de primaria
- **Tecnología:** Usuario intermedio de smartphone
- **Dolor principal:** Su hijo de 9 años pasa horas en YouTube y se niega a apagarlo
- **Motivación:** Quiere que su hijo tenga tiempo para leer, jugar afuera y dormir mejor
- **Cita:** *"No quiero ser la villana de la película cada noche"*

#### Persona 2 — "El Papá Ocupado"
- **Nombre:** Carlos, 42 años
- **Ocupación:** Ingeniero, trabaja desde casa
- **Tecnología:** Usuario avanzado
- **Dolor principal:** No tiene tiempo para supervisar el uso del dispositivo de sus hijas
- **Motivación:** Quiere una solución automática que funcione en segundo plano
- **Cita:** *"Necesito que esto funcione solo, no tengo tiempo para configurar cosas complejas"*

#### Persona 3 — "El Niño Gamer"
- **Nombre:** Mateo, 11 años
- **Tecnología:** Usuario nativo digital
- **Dolor principal:** Le "cortan" el videojuego sin aviso justo cuando está en una partida importante
- **Motivación:** Quiere que sus padres confíen en él y ganar más tiempo
- **Cita:** *"Si me avisan con tiempo, yo mismo lo apago"*

#### Persona 4 — "La Niña Creativa"
- **Nombre:** Sofía, 8 años
- **Tecnología:** Usa tablet para dibujar y ver videos
- **Dolor principal:** No entiende por qué a veces puede usar la tablet y otras no
- **Motivación:** Quiere ser recompensada cuando se porta bien
- **Cita:** *"Si hago mis tareas, ¿puedo tener más tiempo?"*

---

## 6. Alcance del producto (MVP)

### 6.1 Incluido en V1.0

| ID | Funcionalidad | Prioridad |
|---|---|---|
| F-01 | Registro de familia y creación de perfil de hijo (1 hijo en plan gratuito) | P0 |
| F-02 | Vinculación del dispositivo Android del hijo con la cuenta familiar | P0 |
| F-03 | Configuración de límite de tiempo diario por dispositivo | P0 |
| F-04 | Configuración de horarios de descanso (sin pantallas) | P0 |
| F-05 | Notificaciones de aviso al niño (15 min, 5 min, tiempo agotado) | P0 |
| F-06 | Bloqueo del dispositivo al agotar el tiempo | P0 |
| F-07 | Panel del padre: resumen de uso del día | P0 |
| F-08 | Modo Chill: pantalla de desconexión con actividades sugeridas | P0 |
| F-09 | Sistema de solicitud de tiempo extra (niño solicita → padre aprueba) | P0 |
| F-10 | Soporte para múltiples hijos (hasta 6) en plan Familiar | P1 |
| F-11 | Reporte semanal de uso por hijo (plan Familiar) | P1 |

### 6.2 Fuera del alcance de V1.0 (a considerar para V1.1+)

- **Agente para iOS** — el MVP soporta sólo dispositivos Android del hijo. La app del padre sí es multiplataforma.
- **Dashboard web del padre** — toda la gestión se hace desde la app móvil.
- **Sistema de recompensas** (puntos por actividades offline).
- **Co-administradores** (un solo padre/madre por familia en MVP).
- **Control por aplicación individual** (solo control del dispositivo completo).
- **Reportes históricos** más allá de los últimos 7 días en plan gratuito.
- Integración con plataformas educativas externas.
- Modo multi-dispositivo del niño (1 dispositivo por hijo en MVP).
- Localización en idiomas distintos al español e inglés.

---

## 7. Requisitos funcionales

### 7.1 Módulo de autenticación

- **RF-01:** El padre puede registrarse con email/contraseña o Google/Apple Sign-In.
- **RF-02:** La sesión del padre permanece activa hasta que cierre sesión manualmente.
- **RF-03:** El acceso al panel de padres requiere autenticación biométrica o PIN si el dispositivo del niño lo solicita.

### 7.2 Módulo de gestión familiar

- **RF-04:** En el plan gratuito, un padre puede crear 1 perfil de hijo. En el plan Familiar, hasta 6.
- **RF-05:** Cada perfil de hijo incluye: nombre, edad, foto (opcional) y dispositivo vinculado.

### 7.3 Módulo de límites y horarios

- **RF-07:** El padre configura un límite de tiempo diario (en horas y minutos) por perfil de hijo.
- **RF-08:** El límite puede variar según el día de la semana (ej: más tiempo los fines de semana).
- **RF-09:** El padre define horarios de "tiempo sin pantallas" (ej: 21:00 - 07:00).
- **RF-10:** Durante los horarios de descanso, el dispositivo del hijo queda bloqueado independientemente del tiempo restante.

### 7.4 Módulo de monitoreo y notificaciones

- **RF-11:** El agente en el dispositivo del hijo registra el tiempo de uso activo.
- **RF-12:** Se envían notificaciones al niño cuando queda el 25%, 15 minutos y 5 minutos de tiempo.
- **RF-13:** El padre recibe una notificación cuando el hijo agota su tiempo diario.
- **RF-14:** El padre puede ver el tiempo consumido y restante de cada hijo con una latencia máxima de 5 minutos respecto al uso real.
- **RF-15:** El agente cachea localmente las reglas de tiempo y horarios. Si pierde conexión con el backend, sigue aplicando las últimas reglas conocidas y sincroniza el uso acumulado al reconectar (modo offline fail-open).

### 7.5 Módulo de solicitudes

- **RF-16:** El niño puede enviar una solicitud de tiempo extra con un mensaje opcional.
- **RF-17:** El padre recibe la solicitud como notificación push y puede aprobar/rechazar desde cualquier pantalla.
- **RF-18:** El padre puede aprobar un tiempo adicional específico (ej: 30 minutos) o indefinido (hasta el horario de descanso).
- **RF-19:** El niño es notificado inmediatamente del resultado de su solicitud.

### 7.6 Modo Chill

- **RF-20:** Al bloquearse el dispositivo, se muestra una pantalla amigable con el tiempo transcurrido y mensajes positivos.
- **RF-21:** La pantalla de Chill sugiere entre 3 y 5 actividades offline aleatorias apropiadas para la edad.
- **RF-22:** El niño puede marcar una actividad como "en curso" para que el padre lo vea.

---

## 8. Requisitos no funcionales

| ID | Requisito | Criterio de aceptación |
|---|---|---|
| RNF-01 | Rendimiento | El agente de monitoreo no debe consumir más del 3% de batería por hora |
| RNF-02 | Disponibilidad | El servicio backend debe tener un uptime del 99.5% |
| RNF-03 | Latencia | Las notificaciones deben llegar en menos de 5 segundos |
| RNF-04 | Seguridad | Los datos del niño nunca se transmiten a terceros; cumplimiento COPPA y GDPR |
| RNF-05 | Privacidad | No se registra contenido del dispositivo, solo métricas de tiempo |
| RNF-06 | Usabilidad | Un padre sin experiencia técnica debe completar la configuración inicial en < 5 min |
| RNF-07 | Escalabilidad | La arquitectura debe soportar 500,000 familias activas sin rediseño |
| RNF-08 | Compatibilidad (MVP) | Agente del hijo: Android 10+. App del padre: Android 10+ e iOS 15+ |
| RNF-09 | Tolerancia a fallos | Si el agente pierde conexión, sigue aplicando las últimas reglas conocidas y permite el uso normal hasta agotar el tiempo cacheado (no bloquea por desconexión) |

---

## 9. Restricciones y supuestos

### Restricciones
- El bloqueo del dispositivo depende de las APIs de accesibilidad/administración de Android (`UsageStatsManager`, `DevicePolicyManager`, `AccessibilityService`).
- El MVP soporta sólo dispositivos Android del hijo. El soporte iOS requiere el entitlement `FamilyControls` de Apple y queda planificado para V1.1.
- El niño no debe poder desinstalar fácilmente el agente (requiere PIN del padre).

### Supuestos
- Los padres tienen un smartphone con Android 10+ o iOS 15+.
- El hijo tiene un dispositivo Android 10+ propio o compartido.
- La familia tiene conexión a internet al menos esporádicamente (para sincronización). El agente funciona offline con las últimas reglas cacheadas.

---

## 10. Dependencias

- **Firebase Cloud Messaging** — Notificaciones push
- **Android Device Administration API + UsageStatsManager** — Control y monitoreo del dispositivo del hijo
- **Google / Apple Sign-In** — Autenticación social del padre
- **Stripe** — Procesamiento de pagos (plan Familiar)

---

## 11. Modelo de negocio

| Plan | Precio | Límites |
|---|---|---|
| **Gratuito** | $0/mes | 1 hijo, funciones básicas, sin reportes históricos |
| **Familiar** | $4.99/mes | Hasta 6 hijos, todas las funciones, reportes históricos |
| **Anual Familiar** | $39.99/año | Igual que Familiar con 33% de descuento |

---

## 12. Riesgos

| Riesgo | Probabilidad | Impacto | Mitigación |
|---|---|---|---|
| Niños buscan formas de evadir el bloqueo (modo avión, desinstalar, factory reset) | Alta | Medio | PIN de desinstalación, modo administrador de dispositivo, agente reanuda al reconectar |
| Caída del backend deja al hijo sin reglas | Media | Alto | Modo offline fail-open: el agente cachea reglas y sigue aplicándolas localmente (RNF-09) |
| Padres olvidan configurar el sistema | Media | Alto | Onboarding guiado y recordatorios de configuración |
| Conflictos familiares aumentan por mal uso | Baja | Alto | Guía de uso colaborativo incluida en el onboarding |
| Lanzamiento iOS bloqueado por entitlement de Apple | Alta | Medio | iOS está fuera del MVP; se evalúa el entitlement antes de comprometerse a V1.1 |

---

## Historial de versiones

| Versión | Fecha | Autor | Cambios |
|---|---|---|---|
| 1.0 | Mayo 2026 | Equipo ChillTechControl | Documento inicial |
