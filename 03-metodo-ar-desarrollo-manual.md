# Capa III — Método AR sin Vibe Coding (Desarrollo Manual Asistido)

Para vos, cuando el que escribe el código sos vos y no el agente. Las Capas I y II asumen vibe coding: el agente ejecuta, vos supervisás. Acá el reparto es al revés — vos ejecutás, el modelo se consulta puntualmente (revisar un fragmento, discutir una arquitectura, explicar un error). Es el mismo método, con la disciplina aplicada al lado contrario.

---

## 00 — Qué cambia cuando el que escribe sos vos

> Un modelo no piensa. Responde según el contexto que le construyes.

La premisa central no cambia. Lo que cambia es quién actúa sobre esa respuesta.

En vibe coding el riesgo es que **el agente** se desvíe del plan sin que nadie lo note — por eso Capa II insiste en audit trail, detección de desviación, reset de contexto: mecanismos para vigilar a quien ejecuta.

En desarrollo manual asistido el riesgo es el opuesto y más difícil de ver: que **vos** te desvíes de tu propio plan porque una sugerencia del modelo te sonó bien en el momento, y termines con una decisión de arquitectura tomada por reflejo de una respuesta de chat — sin el mismo escrutinio que le exigirías a un agente si hubiera actuado solo. Nadie audita al humano. Por eso hay que autoauditarse a propósito.

> **Regla:** Tratá cada sugerencia del modelo que aceptás como si fuera la decisión propia de un agente — con el mismo peso, la misma pregunta ("¿esto lo pedí yo o me lo convenció el chat?"), el mismo registro.

---

## 01 — El Ciclo AR, con los roles invertidos

| Paso | En vibe coding (Capa II) | En desarrollo manual asistido (acá) |
|---|---|---|
| **PLANEAR** | Le construís el contexto al agente para que actúe | Te construís el contexto a vos mismo — y definís de antemano para qué vas a consultar al modelo (arquitectura, revisión, debugging) y qué vas a resolver solo, sin preguntar |
| **EJECUTAR** | El agente actúa, reporta qué tocó | Vos escribís. Cada vez que una respuesta del modelo cambia lo que ibas a hacer, es una decisión — tuya, influenciada — y se registra igual que P-09/P-10 |
| **AUDITAR** | Le preguntás al agente cuánto se desvió | Te preguntás a vos mismo: ¿cuánto de lo que hice hoy vino de aceptar una sugerencia sin cuestionarla? |
| **DETECTAR** | Dos iteraciones del agente fallando = contexto contaminado | Dos intentos tuyos fallando en lo mismo = tu propio hilo de hipótesis está contaminado, no el context window de nadie |
| **RESETEAR** | Chat nuevo, memoria selectiva | Vos parás, anotás qué sabés y qué no, y volvés con la cabeza fresca — el "reset" es tuyo, no de una ventana de contexto |

La sección 4 (v1) de Capa II — "Cuándo NO usar un agente" — aplica igual acá: si el proceso no está documentado, si el conocimiento es tácito, si el fallo es irreversible. Esas condiciones no dependen de quién escribe el código.

---

## 02 — Qué patrones de la Capa II aplican, cuáles se traducen, cuáles no

| Patrón | Estado en desarrollo manual | Traducción |
|---|---|---|
| P-01 — Compresión de contexto | Aplica directo | El mapa de 150 líneas te sirve a vos igual que a un agente — no lo escribís para "el agente lea menos", lo escribís para pensar con la abstracción correcta |
| P-01b — Arquitectura por audiencia | Aplica directo | Índice, estado, bitácora, plan por bloque — la separación no depende de quién ejecuta |
| P-02/P-03/P-09/P-10 — Decisión propia (y su gradiente) | Se traduce | "Decisión propia del agente" pasa a ser "decisión mía influenciada por el modelo". El gradiente (cosmética / técnica-interna / de producto) se mantiene; lo que cambia es que el "acuerdo antes de codear" (P-10) ahora es con vos mismo o tu equipo, no con quien te pidió la tarea |
| P-04 — Reset de contexto | Se traduce | No hay ventana de contexto que limpiar — hay tu propia cabeza. Señal idéntica (dos iteraciones fallando), remedio distinto: parar, anotar, descansar, no seguir adivinando |
| P-05/P-06 — Versionado de contexto, anclas estables | Aplica directo | Tu documentación se desactualiza igual de rápido si nadie la toca — más todavía si no hay un agente que la lea antes de cada sesión y note el desfase |
| P-07 — Case study de desviación | Aplica directo | Un bug tuyo con dos rondas fallidas también merece postmortem — la disciplina de "no cerrar con 'ya funciona'" no es solo para agentes |
| P-08 — Alcance explícito del bloque | Aplica directo | Vos también "mejorás" cosas fuera de alcance sin darte cuenta cuando programás solo |
| P-11 — Bitácora de reversión | Aplica directo | Lo que probaste, construiste y descartaste vale igual documentado, seas vos o un agente quien lo escribió |
| P-12 — Secretos fuera del contexto | Se endurece | Ni siquiera para "que el modelo me ayude a debuggear" pegás un token o una clave en el chat — la tentación es mayor cuando sos vos quien decide pegar, no un agente actuando por su cuenta |
| P-13 — Convención de nombres | Aplica directo | No depende de quién escribe el código, depende de que alguien lo vuelva a leer en seis semanas |

**Lo que no aplica:** P-04 tal como está escrito ("context window reset") es literal para LLMs; acá es metáfora. Y el "audit trail por iteración" (P-02) pierde su forma original — no hay a quién pedirle que reporte, el reporte lo escribís vos, lo cual es más fácil de saltarse. Por eso el punto 03 lo convierte en checklist.

---

## 03 — Checklist de bolsillo (para vos, no para pegarle a un agente)

**Antes de sentarte a programar:**
- [ ] Tengo mi propio mapa de 150 líneas del proyecto, no todo en la cabeza
- [ ] Sé para qué voy a consultar al modelo hoy y para qué no
- [ ] Sé qué NO entra en este bloque

**Mientras programás, si consultás al modelo:**
- [ ] Antes de aceptar una sugerencia que cambia tu plan: ¿es cosmética, técnica-interna o de producto? Si es de producto, pensala vos antes de escribirla, no la copies porque sonó bien
- [ ] Ningún secreto entra al chat, ni para pedir ayuda a debuggear

**Al cerrar el bloque:**
- [ ] ¿Cuánto de lo de hoy vino de una sugerencia que no cuestioné?
- [ ] Si construí algo y lo descarté, quedó anotado igual que lo que sí quedó
- [ ] Si dos intentos seguidos fallé en lo mismo: paré, anoté, no seguí adivinando en el tercero

---

*Construido desde Socorro, Santander 🇨🇴*
