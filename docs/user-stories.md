# Historias de Usuario
# ChillTechControl

**Versión:** 1.0  
**Fecha:** Mayo 2026

---

## Convención

```
Como [rol],
quiero [acción/funcionalidad],
para [beneficio/objetivo].

Criterios de aceptación:
  - DADO [contexto], CUANDO [acción], ENTONCES [resultado esperado]
```

**Prioridades:** 🔴 Must Have (MVP) | 🟡 Should Have | 🟢 Nice to Have

---

## Épica 1: Registro y configuración de familia

### US-01 — Registro del padre 🔴
**Como** padre o madre,  
**quiero** crear una cuenta en ChillTechControl con mi email o cuenta de Google/Apple,  
**para** tener un perfil donde gestionar los dispositivos de mis hijos.

**Criterios de aceptación:**
- DADO que soy un usuario nuevo, CUANDO ingreso mi email y una contraseña segura, ENTONCES se crea mi cuenta y recibo un email de verificación.
- DADO que tengo Google/Apple Sign-In disponible, CUANDO elijo esa opción, ENTONCES inicio sesión sin necesidad de contraseña adicional.
- DADO que intento registrarme con un email ya existente, ENTONCES recibo un mensaje indicando que la cuenta ya existe.

---

### US-02 — Creación de perfil de hijo 🔴
**Como** padre,  
**quiero** crear un perfil para cada uno de mis hijos con su nombre y edad,  
**para** aplicar reglas personalizadas según las necesidades de cada niño.

**Criterios de aceptación:**
- DADO que estoy en el panel de padres, CUANDO pulso "Agregar hijo", ENTONCES puedo ingresar nombre, edad y foto opcional.
- DADO que creo el perfil, CUANDO lo guardo, ENTONCES aparece en mi lista de hijos con su tiempo de uso configurado por defecto.
- DADO que estoy en el plan gratuito y ya tengo 1 hijo creado, CUANDO intento agregar otro, ENTONCES se me muestra una invitación a actualizar al plan Familiar.
- DADO que estoy en el plan Familiar, CUANDO intento crear el perfil número 7, ENTONCES recibo un mensaje indicando el límite de 6 perfiles.

---

### US-03 — Vinculación del dispositivo del hijo 🔴
**Como** padre,  
**quiero** vincular el dispositivo Android de mi hijo a su perfil,  
**para** que la aplicación pueda monitorear y controlar su tiempo de uso.

**Criterios de aceptación:**
- DADO que tengo el dispositivo Android del hijo en mano, CUANDO instalo el agente ChillTechControl y escaneo el QR desde el panel de padres, ENTONCES el dispositivo queda vinculado al perfil del hijo.
- DADO que el dispositivo está vinculado, CUANDO el niño usa el dispositivo, ENTONCES el tiempo activo se registra y se sincroniza con el backend.
- DADO que el padre intenta desvincular el dispositivo, ENTONCES se requiere confirmar con su contraseña o biometría.

---

## Épica 2: Gestión de límites de tiempo

### US-04 — Configurar límite de tiempo diario 🔴
**Como** padre,  
**quiero** establecer cuántas horas al día puede usar el dispositivo mi hijo,  
**para** evitar el uso excesivo sin tener que intervenir manualmente cada día.

**Criterios de aceptación:**
- DADO que abro el perfil de un hijo, CUANDO configuro el límite diario, ENTONCES puedo elegir horas y minutos (mínimo 30 min, máximo 12 horas).
- DADO que establezco límites diferentes por día de semana, ENTONCES el sistema aplica el límite correspondiente automáticamente.
- DADO que el niño agota su tiempo, ENTONCES el dispositivo se bloquea y se activa el Modo Chill.

---

### US-05 — Configurar horarios sin pantallas 🔴
**Como** padre,  
**quiero** definir franjas horarias en las que el dispositivo esté siempre bloqueado,  
**para** proteger el tiempo de sueño, las comidas y el tiempo familiar.

**Criterios de aceptación:**
- DADO que configuro un horario de descanso (ej. 21:00 - 07:00), CUANDO llega esa hora, ENTONCES el dispositivo del hijo se bloquea aunque tenga tiempo disponible.
- DADO que el horario de descanso está activo, CUANDO el niño intenta usar el dispositivo, ENTONCES ve el Modo Chill con el mensaje "Es hora de descansar".
- DADO que el padre quiere hacer una excepción, ENTONCES puede desactivar el horario temporalmente desde su app con su PIN.

---

### US-06 — Ver y modificar límites 🟡
**Como** padre,  
**quiero** poder revisar y ajustar fácilmente los límites de cada hijo,  
**para** adaptarlos si hay cambios en la rutina familiar (vacaciones, enfermedad, etc.).

**Criterios de aceptación:**
- DADO que abro el perfil de un hijo, CUANDO veo los límites actuales, ENTONCES están visualmente claros y puedo modificarlos con pocos toques.
- DADO que modifico un límite, CUANDO guardo los cambios, ENTONCES se aplican en el dispositivo del hijo en menos de 10 segundos.

---

## Épica 3: Monitoreo y reportes

### US-07 — Ver tiempo de uso en tiempo real 🔴
**Como** padre,  
**quiero** saber en todo momento cuánto tiempo ha usado hoy mi hijo el dispositivo,  
**para** tener conciencia de sus hábitos sin tener que preguntarle o revisar el dispositivo.

**Criterios de aceptación:**
- DADO que abro el panel de padres, CUANDO selecciono a un hijo, ENTONCES veo el tiempo usado hoy y el tiempo restante en una visualización clara.
- DADO que el niño está usando el dispositivo en ese momento, ENTONCES el contador refleja el uso real con una latencia máxima de 5 minutos (alineado con la frecuencia de heartbeat del agente).

---

### US-08 — Reporte semanal 🟡
**Como** padre,  
**quiero** recibir un resumen semanal del uso de pantalla de mis hijos,  
**para** identificar tendencias y tener conversaciones informadas con ellos.

**Criterios de aceptación:**
- DADO que ha pasado una semana, CUANDO recibo el reporte, ENTONCES incluye: tiempo total por día, días que superó el límite, actividad en Modo Chill.
- DADO que veo el reporte, CUANDO lo comparo con la semana anterior, ENTONCES puedo ver si el tiempo aumentó o disminuyó.
- DADO que soy usuario del plan gratuito, ENTONCES tengo acceso solo al reporte de los últimos 7 días.

---

### US-09 — Historial de uso del hijo (vista del niño) 🟡
**Como** niño,  
**quiero** ver cuánto tiempo he usado hoy y esta semana,  
**para** ser consciente de mis propios hábitos y sentirme más responsable.

**Criterios de aceptación:**
- DADO que abro la app en mi dispositivo, CUANDO veo mi pantalla principal, ENTONCES veo mi tiempo de hoy en un diseño amigable y visual (barra, emoji, etc.).
- DADO que quiero ver mi semana, CUANDO deslizo hacia el resumen semanal, ENTONCES veo un gráfico de barras simple con mis días.

---

## Épica 4: Notificaciones y bloqueo

### US-10 — Recibir avisos antes del bloqueo 🔴
**Como** niño,  
**quiero** recibir avisos cuando mi tiempo esté por terminarse,  
**para** poder guardar mi progreso o terminar lo que estoy haciendo antes de que se bloquee.

**Criterios de aceptación:**
- DADO que me quedan 15 minutos, ENTONCES recibo una notificación push y una superposición visual en la pantalla.
- DADO que me quedan 5 minutos, ENTONCES la notificación es más prominente (sonido + vibración configurable).
- DADO que mi tiempo se agota, ENTONCES el dispositivo muestra el Modo Chill, no simplemente se apaga sin aviso.

---

### US-11 — Experiencia de bloqueo (Modo Chill) 🔴
**Como** niño,  
**quiero** que cuando se acabe mi tiempo, la pantalla me muestre algo amigable y no solo una pantalla en negro,  
**para** no sentirlo como un castigo sino como una transición natural.

**Criterios de aceptación:**
- DADO que mi tiempo se agota, CUANDO se activa el bloqueo, ENTONCES veo una pantalla con un mensaje positivo, mi tiempo usado hoy y sugerencias de actividades offline.
- DADO que estoy en Modo Chill, CUANDO elijo una actividad sugerida, ENTONCES queda registrada y mi padre puede verla.
- DADO que intento salir del Modo Chill, ENTONCES solo puedo hacerlo si queda tiempo disponible o el padre desbloquea.

---

## Épica 5: Sistema de solicitudes (negociación)

### US-12 — Solicitar tiempo extra 🔴
**Como** niño,  
**quiero** poder pedirle a mis padres que me den más tiempo cuando se me acabe,  
**para** poder terminar algo importante sin tener que interrumpirles físicamente.

**Criterios de aceptación:**
- DADO que estoy en el Modo Chill, CUANDO pulso "Pedir más tiempo", ENTONCES puedo escribir un mensaje corto y enviar la solicitud.
- DADO que envío la solicitud, ENTONCES mi padre recibe una notificación inmediata con mi mensaje.
- DADO que mi padre responde, ENTONCES recibo una notificación con el resultado (aprobado/rechazado y tiempo concedido).

---

### US-13 — Aprobar o rechazar solicitud de tiempo extra 🔴
**Como** padre,  
**quiero** recibir y responder solicitudes de tiempo extra de mis hijos rápidamente,  
**para** mantener el control sin tener que estar físicamente junto a ellos.

**Criterios de aceptación:**
- DADO que mi hijo solicita más tiempo, CUANDO recibo la notificación, ENTONCES puedo ver su mensaje y elegir aprobar con un tiempo específico o rechazar.
- DADO que apruebo la solicitud, CUANDO confirmo la cantidad de tiempo extra, ENTONCES el dispositivo del hijo se desbloquea automáticamente.
- DADO que rechazo la solicitud, ENTONCES puedo agregar un mensaje opcional explicando por qué.

---

## Épica 6: Sistema de recompensas

### US-14 — Ganar tiempo extra completando actividades 🟡
**Como** niño,  
**quiero** poder ganar tiempo de pantalla adicional completando actividades que mis padres valoran,  
**para** sentir que tengo control sobre mi tiempo y que mi esfuerzo es reconocido.

**Criterios de aceptación:**
- DADO que hay una tarea disponible (ej. "Leer 30 minutos"), CUANDO la marco como completada, ENTONCES queda pendiente de verificación del padre.
- DADO que el padre verifica la actividad, CUANDO la aprueba, ENTONCES se acredita el tiempo de recompensa a mi saldo del día.
- DADO que acumulo tiempo de recompensa, ENTONCES puede aplicarse al día actual o guardarse para otro día.

---

### US-15 — Configurar actividades recompensadas 🟡
**Como** padre,  
**quiero** definir qué actividades offline le dan tiempo extra a mi hijo,  
**para** incentivar comportamientos que valoro (lectura, ejercicio, tareas del hogar).

**Criterios de aceptación:**
- DADO que abro la sección de recompensas del perfil de mi hijo, CUANDO creo una actividad, ENTONCES defino: nombre, descripción y minutos de recompensa.
- DADO que una actividad está configurada, ENTONCES aparece disponible en la pantalla del niño.
- DADO que quiero desactivar temporalmente una actividad, ENTONCES puedo pausarla sin eliminarla.

---

## Épica 7: Configuración y accesibilidad

### US-16 — Funcionamiento offline del agente 🔴
**Como** padre,  
**quiero** que el control siga funcionando aunque se pierda la conexión a internet,  
**para** que un fallo del backend o de la red no signifique que mi hijo pierda el control de tiempo.

**Criterios de aceptación:**
- DADO que el agente tiene reglas cacheadas, CUANDO pierde conexión con el backend, ENTONCES sigue aplicando los límites diarios y horarios de descanso conocidos.
- DADO que el agente está offline, CUANDO acumula tiempo de uso, ENTONCES lo guarda localmente y lo sincroniza al reconectar.
- DADO que el agente recupera la conexión, CUANDO recibe nuevas reglas, ENTONCES las aplica en menos de 10 segundos.

---

### US-17 — Proteger la configuración con PIN 🔴
**Como** padre,  
**quiero** que el niño no pueda cambiar la configuración ni desinstalar el agente fácilmente,  
**para** asegurar que los límites se respeten.

**Criterios de aceptación:**
- DADO que el niño intenta desinstalar el agente, ENTONCES se requiere el PIN del padre.
- DADO que el niño intenta acceder a la configuración del agente, ENTONCES también se requiere el PIN.
- DADO que el padre olvida el PIN, ENTONCES puede recuperarlo desde la app de padres con su autenticación.

---

### US-18 — Modo multi-idioma 🟢
**Como** usuario,  
**quiero** usar la aplicación en mi idioma preferido (español o inglés),  
**para** entender todas las funciones correctamente.

**Criterios de aceptación:**
- DADO que instalo la app, CUANDO el idioma del sistema es español, ENTONCES la app se muestra en español por defecto.
- DADO que quiero cambiar el idioma, CUANDO voy a configuración, ENTONCES puedo elegir entre español e inglés.

---

## Resumen de historias por épica

| Épica | Historias | MVP |
|---|---|---|
| Registro y familia | US-01, US-02, US-03 | ✅ Todas |
| Límites de tiempo | US-04, US-05, US-06 | US-04, US-05 son MVP |
| Monitoreo y reportes | US-07, US-08, US-09 | US-07 es MVP |
| Notificaciones y bloqueo | US-10, US-11 | ✅ Todas |
| Sistema de solicitudes | US-12, US-13 | ✅ Todas |
| Sistema de recompensas | US-14, US-15 | ❌ V1.1+ |
| Configuración y resiliencia | US-16, US-17, US-18 | US-16, US-17 son MVP |

**Total historias MVP:** 12  
**Total historias V1.1+:** 6
