# Flujos de Usuario y Diseño UX
# ChillTechControl

**Versión:** 1.0  
**Fecha:** Mayo 2026

---

## 1. Principios de diseño UX

| Principio | Aplicación |
|---|---|
| **Positivo, no punitivo** | Colores cálidos, mensajes amigables; nunca texto de "error" o "bloqueado" en la vista del niño |
| **Edad adaptativa** | La UI del niño varía según su edad (4-6, 7-10, 11-16) con más texto y menos iconos en edades mayores |
| **Transparencia** | El niño siempre sabe cuánto tiempo le queda y por qué hay un límite |
| **Mínimos pasos** | Los flujos del padre no deben superar 3 pasos para cualquier acción frecuente |
| **Accesibilidad** | Contraste mínimo WCAG AA, soporte de tamaño de texto del sistema, labels para lectores de pantalla |

---

## 2. Flujo de onboarding del padre

```
┌──────────────────────────────────────────────────────┐
│                   ONBOARDING PADRE                    │
└──────────────────────────────────────────────────────┘

  [Pantalla de bienvenida]
        │
        ▼
  ¿Ya tienes cuenta?
        │
   ┌────┴────┐
  Sí        No
   │          │
   ▼          ▼
[Login]    [Registro]
   │       Email + Nombre + Contraseña
   │       ─── ó ───
   │       Google / Apple Sign-In
   │          │
   └────┬─────┘
        │
        ▼
  [Verificación de email]
  (si fue por email/contraseña)
        │
        ▼
  [Crear familia]
  Nombre de la familia (opcional)
        │
        ▼
  [Agregar primer hijo]
  Nombre + Edad + Foto (opcional)
        │
        ▼
  [Instalar agente en el dispositivo del hijo]
  ┌──────────────────────────────────────┐
  │  1. Descarga ChillTechControl Kids  │
  │     en el dispositivo del niño      │
  │  2. Abre la app en el dispositivo   │
  │  3. Escanea este código QR          │
  │         ┌──────────┐               │
  │         │  [QR]    │               │
  │         └──────────┘               │
  └──────────────────────────────────────┘
        │
        ▼
  [Configurar límites básicos]
  ┌─────────────────────────────────────┐
  │  Tiempo diario: [  2  ] horas      │
  │                                     │
  │  Horario de descanso:               │
  │  De [21:00] a [07:00]              │
  └─────────────────────────────────────┘
        │
        ▼
  [¡Listo! Panel principal]
```

**Notas UX:**
- El paso de instalación del agente incluye instrucciones paso a paso con capturas de pantalla.
- Si el padre salta el paso del agente, puede completarlo después desde el panel.
- La configuración de límites tiene valores sugeridos según la edad del niño (ej: 8 años → 1.5h recomendado).

---

## 3. Panel principal del padre

```
┌────────────────────────────────────────────┐
│  ChillTechControl          🔔  👤          │
│                                            │
│  Hoy, jueves 8 de mayo                    │
│                                            │
│  ┌──────────────────────────────────────┐  │
│  │  👧 Sofía, 8 años                   │  │
│  │  ████████░░░░  1h 45min / 2h        │  │
│  │  Tiempo restante: 15 min  ⚠️         │  │
│  └──────────────────────────────────────┘  │
│                                            │
│  ┌──────────────────────────────────────┐  │
│  │  🧒 Mateo, 11 años                  │  │
│  │  ████░░░░░░░░  45min / 3h           │  │
│  │  Tiempo restante: 2h 15min  ✅       │  │
│  └──────────────────────────────────────┘  │
│                                            │
│  ┌──────────────────────────────────────┐  │
│  │  📬 Solicitudes pendientes: 1        │  │
│  │  Sofía pide 30 min más              │  │
│  │  [Aprobar]  [Rechazar]  [Ver]       │  │
│  └──────────────────────────────────────┘  │
│                                            │
│  [📊 Reporte semanal]  [⚙️ Configurar]    │
└────────────────────────────────────────────┘
```

**Notas UX:**
- La barra de progreso cambia de color: verde (>50%), amarillo (25-50%), rojo (<25%).
- Las tarjetas de hijos son pulsables para ir al detalle del hijo.
- Las solicitudes pendientes tienen prioridad visual alta.
- Notificación badge en el ícono de campana cuando hay alertas nuevas.

---

## 4. Detalle del perfil del hijo (vista del padre)

```
┌────────────────────────────────────────────┐
│  ←  Sofía                            ⚙️   │
│                                            │
│           👧  Sofía                        │
│           8 años                          │
│                                            │
│  HOY                                       │
│  ┌──────────────────────────────────────┐  │
│  │  Tiempo usado: 1h 45min             │  │
│  │  Tiempo restante: 15 min            │  │
│  │  ████████████░░  88%               │  │
│  └──────────────────────────────────────┘  │
│                                            │
│  REGLAS ACTIVAS                           │
│  ┌──────────────────────────────────────┐  │
│  │  ⏱  Límite diario: 2 horas          │  │
│  │  🌙  Descanso: 21:00 - 07:00        │  │
│  │              [Editar reglas]         │  │
│  └──────────────────────────────────────┘  │
│                                            │
│  ESTA SEMANA                              │
│  Lun  Mar  Mié  Jue  Vie  Sáb  Dom       │
│  ██   ██   ███  ██   -    -    -          │
│  1h   1h   2h   2h                       │
│                                            │
│  [Ver reporte completo]                   │
│                                            │
│  ACCIONES RÁPIDAS                         │
│  [+ Dar 30 min extra]  [Bloquear ahora]   │
└────────────────────────────────────────────┘
```

---

## 5. Flujo de configuración de reglas

```
[Perfil del hijo] → [Editar reglas]
        │
        ▼
┌────────────────────────────────────────────┐
│  ←  Reglas de Sofía                       │
│                                            │
│  TIEMPO DIARIO                            │
│  ┌──────────────────────────────────────┐  │
│  │  Igual todos los días               │  │
│  │  [2 horas  ▼]                       │  │
│  │                                      │  │
│  │  ○ Diferente por día                │  │
│  └──────────────────────────────────────┘  │
│                                            │
│  HORARIOS SIN PANTALLAS                   │
│  ┌──────────────────────────────────────┐  │
│  │  + Agregar horario                  │  │
│  │                                      │  │
│  │  🌙 Noche    21:00 - 07:00  [━━━]   │  │
│  │  🍽️ Cena     19:30 - 20:30  [━━━]   │  │
│  └──────────────────────────────────────┘  │
│                                            │
│  NOTIFICACIONES AL NIÑO                   │
│  ┌──────────────────────────────────────┐  │
│  │  Avisar cuando queden:              │  │
│  │  ☑ 15 minutos                       │  │
│  │  ☑ 5 minutos                        │  │
│  │  ☑ Tiempo agotado                   │  │
│  └──────────────────────────────────────┘  │
│                                            │
│         [Guardar cambios]                  │
└────────────────────────────────────────────┘
```

---

## 6. Experiencia del niño — Pantalla principal

La app del niño tiene 3 variantes visuales según la edad:

### Versión 4-6 años (muy visual)
```
┌────────────────────────────────────────────┐
│                                            │
│         🌟 ¡Hola, Sofía! 🌟               │
│                                            │
│              😊                           │
│    Tu tiempo de hoy:                      │
│                                            │
│         ╔══════════╗                      │
│         ║  ⏰ 15   ║                      │
│         ║ minutos  ║                      │
│         ╚══════════╝                      │
│                                            │
│    ████████░░░░  casi terminado!          │
│                                            │
│         [¿Qué puedo hacer?]               │
└────────────────────────────────────────────┘
```

### Versión 7-10 años
```
┌────────────────────────────────────────────┐
│  ChillTech                         Sofía   │
│                                            │
│  Tu tiempo de hoy                         │
│  ████████████░░░░░░  1h 45min usados      │
│  Te quedan: 15 minutos                    │
│                                            │
│  Horario de descanso:                     │
│  🌙 Empieza a las 21:00                   │
│                                            │
│  [Pedir más tiempo]                       │
└────────────────────────────────────────────┘
```

> *La sección "Actividades para ganar tiempo" llegará con el sistema de recompensas en V1.1.*

### Versión 11-16 años
```
┌────────────────────────────────────────────┐
│  ChillTechControl                Sofía  ⚙️  │
│                                            │
│  Tiempo disponible hoy                    │
│  ┌──────────────────────────────────────┐  │
│  │  15 min restantes de 2h             │  │
│  │  ███████████████░  88% usado        │  │
│  └──────────────────────────────────────┘  │
│                                            │
│  Esta semana: 7h 30min / 14h límite       │
│                                            │
│  [Solicitar tiempo extra]                 │
│                                            │
│  Próximo bloqueo: Hoy 21:00 (en 3h 15m)  │
└────────────────────────────────────────────┘
```

---

## 7. Modo Chill (pantalla de bloqueo del niño)

```
┌────────────────────────────────────────────┐
│                                            │
│           🌿  Modo Chill  🌿               │
│                                            │
│      ¡Buen trabajo, Sofía!                │
│   Hoy usaste tu tiempo al máximo 😊       │
│                                            │
│   Tiempo usado hoy: 2 horas               │
│                                            │
│   ┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄            │
│                                            │
│   ¿Qué puedes hacer ahora?               │
│                                            │
│   🎨 Dibujar o colorear                   │
│   📚 Leer un libro                        │
│   🎲 Jugar un juego de mesa              │
│   🌳 Salir a caminar                      │
│   🎵 Escuchar música o bailar             │
│                                            │
│   [¡Voy a intentarlo!]                   │
│                                            │
│   ┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄            │
│                                            │
│   ¿Necesitas más tiempo?                  │
│   [Pedirle a mamá/papá]                  │
│                                            │
└────────────────────────────────────────────┘
```

**Notas UX:**
- Fondo con animación suave (ondas, naturaleza).
- No hay botón de "cerrar" ni de "desbloquear" sin permiso del padre.
- El botón de llamada de emergencia siempre está accesible (no se bloquea).
- Los mensajes rotan con frases positivas y no repetitivas.

---

## 8. Flujo de solicitud de tiempo extra

```
NIÑO                                    PADRE
  │                                       │
  │  [Toca "Pedirle a mamá/papá"]        │
  ▼                                       │
[Escribe mensaje]                         │
  "Estoy en mitad de una tarea"          │
  [Enviar solicitud]                      │
  │                                       │
  │ ─────── notificación push ──────────▶ │
  │                                       ▼
  │                              [Notificación recibida]
  │                              "Sofía pide 30 min más"
  │                              "Estoy en mitad de una tarea"
  │                                       │
  │                              [Ver solicitud]
  │                              ┌────────────────┐
  │                              │  ¿Cuánto dar?  │
  │                              │  [15 min]      │
  │                              │  [30 min]      │
  │                              │  [1 hora]      │
  │                              │  [Personalizar]│
  │                              │  [Rechazar]    │
  │                              └────────────────┘
  │                                       │
  │ ◀──────── notificación push ──────── │
  ▼                                       │
[Resultado en Modo Chill]                 │
"¡Mamá te dio 30 minutos extra! 🎉"      │
  │                                       │
  ▼                                       │
[Dispositivo desbloqueado]               │
  │                                       │
  ▼
[Contador continúa con +30 min]
```

---

## 9. Paleta de colores y tipografía

### Colores

| Token | Hex | Uso |
|---|---|---|
| `primary` | `#4ECDC4` | Botones principales, barras de progreso |
| `primary-dark` | `#2BB5AC` | Hover / estados activos |
| `accent` | `#FFD166` | Recompensas, logros, elementos positivos |
| `warning` | `#FF9F43` | Tiempo bajo (<25%) |
| `danger` | `#FF6B6B` | Tiempo agotado (solo en vista del padre) |
| `chill-bg` | `#E8F5E9` | Fondo del Modo Chill |
| `chill-accent` | `#81C784` | Elementos del Modo Chill |
| `neutral-50` | `#FAFAFA` | Fondos generales |
| `neutral-700` | `#374151` | Texto principal |

### Tipografía

| Uso | Familia | Peso | Tamaño |
|---|---|---|---|
| Títulos principales | Inter | 700 | 24-32px |
| Subtítulos | Inter | 600 | 18-20px |
| Cuerpo | Inter | 400 | 14-16px |
| Labels pequeños | Inter | 400 | 12px |
| UI del niño (4-6 años) | Nunito | 700 | 20-28px |

---

## 10. Flujo de navegación — App del padre

```
                      ┌──────────┐
                      │  Login   │
                      └────┬─────┘
                           │
                      ┌────▼─────┐
              ┌───────│  Home    │────────┐
              │       │ Dashboard│        │
              │       └────┬─────┘        │
              │            │              │
              ▼            ▼              ▼
    ┌──────────────┐  ┌──────────┐  ┌──────────┐
    │ Detalle hijo │  │Solicitudes│  │Reportes  │
    └──────┬───────┘  └──────────┘  └──────────┘
           │
    ┌──────▼───────┐
    │ Editar reglas │
    └──────────────┘
```

---

## 11. Mensajes de sistema — Guía de tono

| Situación | ❌ No usar | ✅ Usar |
|---|---|---|
| Tiempo agotado (niño) | "Acceso bloqueado" | "¡Tiempo de descansar! 🌿" |
| Tiempo bajo (niño) | "Advertencia: 15 min restantes" | "Casi terminamos por hoy: 15 minutitos más 😊" |
| Solicitud rechazada (niño) | "Solicitud denegada" | "Mamá/Papá dice que por ahora no, ¡pero sigues siendo genial! 💪" |
| Error de conexión | "Error de red" | "Ups, perdimos la conexión. Volvemos pronto 🔄" |
| Configuración guardada (padre) | "Operación exitosa" | "¡Reglas actualizadas! Los cambios se aplicarán en segundos." |
