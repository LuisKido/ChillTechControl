# ChillTechControl

![Estado](https://img.shields.io/badge/estado-en%20dise%C3%B1o-blue) ![Fase](https://img.shields.io/badge/fase-MVP-orange) ![Licencia](https://img.shields.io/badge/licencia-MIT-green)

> **Controla el tiempo de pantalla. Gana tiempo de vida.**

ChillTechControl es una aplicación multiplataforma que permite a padres e hijos gestionar de forma colaborativa el tiempo de uso de dispositivos tecnológicos, promoviendo pausas saludables y un desarrollo infantil más equilibrado.

---

## ¿Por qué ChillTechControl?

El uso excesivo de dispositivos digitales en la infancia está vinculado a problemas de sueño, dificultades de atención, sedentarismo y menor interacción social. Sin embargo, prohibir la tecnología no es la solución: el objetivo es enseñar a los niños a relacionarse con ella de forma sana.

ChillTechControl nace para:

- Dar a los **padres** visibilidad y control sobre el tiempo de pantalla sin convertirse en "policías digitales".
- Dar a los **niños** autonomía progresiva y conciencia sobre sus propios hábitos.
- Crear **momentos de desconexión** que el niño experimente como algo positivo, no como un castigo.

---

## Características principales

| Funcionalidad | Descripción |
|---|---|
| 🕐 Límites de tiempo diarios | Configura cuántas horas al día puede usar el dispositivo |
| 📅 Horarios de descanso | Define franjas horarias sin pantallas (comidas, hora de dormir, tiempo en familia) |
| 📊 Reportes de uso | Resumen del tiempo consumido por día (reportes históricos en plan Familiar) |
| 🔔 Alertas amigables | Notificaciones graduales que avisan al niño que su tiempo está terminando |
| 🤝 Modo negociación | El niño puede solicitar tiempo adicional; el padre aprueba o rechaza desde su dispositivo |
| 🎮 Perfiles por hijo | Reglas independientes para cada niño según su edad y necesidades |
| 🌙 Modo Chill | Bloqueo suave del dispositivo con actividades alternativas sugeridas (respiración, lectura, juego offline) |

---

## Estructura del repositorio

```
ChillTechControl/
├── README.md
├── docs/
│   ├── prd.md                  # Product Requirements Document
│   ├── user-stories.md         # Historias de usuario
│   ├── architecture.md         # Arquitectura técnica
│   └── ux-flows.md             # Flujos de usuario y wireframes
├── src/
│   ├── app/                    # Aplicación móvil del padre (React Native, iOS + Android)
│   ├── backend/                # API y servicios (Node.js + TypeScript)
│   └── agent/                  # Agente de monitoreo (Android nativo, Kotlin)
├── infra/
│   └── ...                     # Infraestructura (Docker, CI/CD)
└── tests/
    └── ...                     # Tests unitarios, integración y e2e
```

---

## Stack tecnológico (planificado)

- **App del padre:** React Native (iOS & Android)
- **Agente del niño (MVP):** Kotlin nativo (Android 10+). iOS queda para V1.1.
- **Backend:** Node.js + TypeScript + NestJS
- **Base de datos:** PostgreSQL (datos de usuarios) + Redis (sesiones y caché)
- **Notificaciones:** Firebase Cloud Messaging
- **Infraestructura:** Docker, GitHub Actions CI/CD

> **Fuera del MVP:** dashboard web, agente iOS, control por aplicación individual, sistema de recompensas, co-administradores.

---

## Documentación

| Documento | Descripción |
|---|---|
| [PRD](docs/prd.md) | Requisitos del producto, objetivos y métricas de éxito |
| [User Stories](docs/user-stories.md) | Historias de usuario por rol |
| [Arquitectura](docs/architecture.md) | Diagrama y decisiones de arquitectura técnica |
| [Flujos UX](docs/ux-flows.md) | Flujos de navegación y wireframes conceptuales |

---

## Roles en la aplicación

```
┌─────────────────────────────────────────────┐
│                ChillTechControl             │
│                                             │
│   👨‍👩‍👧  Padre / Madre (Admin)                  │
│   └── Configura reglas y límites            │
│   └── Aprueba solicitudes de tiempo extra   │
│   └── Recibe reportes de uso                │
│                                             │
│   👧  Hijo/a (Usuario controlado)           │
│   └── Ve su tiempo disponible              │
│   └── Solicita extensiones                 │
│   └── Desbloquea logros                    │
│                                             │
│   🧑‍💻  Dispositivo (Agente)                  │
│   └── Monitorea tiempo de uso              │
│   └── Aplica bloqueos según reglas         │
│   └── Reporta datos al backend             │
└─────────────────────────────────────────────┘
```

---

## Principios de diseño

1. **Positivo, no punitivo** — Los bloqueos no son castigos; son invitaciones a otras actividades.
2. **Transparente para el niño** — El niño siempre sabe cuánto tiempo le queda y por qué se activan los límites.
3. **Colaborativo** — Los límites se construyen en conversación entre padres e hijos, no impuestos unilateralmente.
4. **Privacidad primero** — No se graba contenido del dispositivo del niño; solo se monitoran métricas de tiempo de uso.
5. **Progresivo** — A medida que el niño demuestra autocontrol, puede ganar más autonomía.

---

## Licencia

MIT © 2026 ChillTechControl Team
