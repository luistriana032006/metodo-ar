# Método AR

Framework para construir, operar y escalar sistemas agénticos.

> Un modelo no piensa. Responde según el contexto que le construyes. Por lo tanto, tu trabajo no es explicarle la tarea — es construir el contexto correcto.

**Autor:** Luis Miguel Triana Rueda — Socorro, Santander, Colombia — GCI World / Trident-AI
**Versión:** v3.0 (sin publicar) — ver [`CHANGELOG.md`](./CHANGELOG.md)

---

## Premisa central

Este documento no es un manual de herramientas. Es un conjunto de principios descubiertos en la práctica real de construir software con agentes de IA — sin academia que los enseñe, sin curso que los sistematice.

El Método AR se organiza en tres capas complementarias. La primera es para quienes toman decisiones sobre agentificación empresarial. La segunda es para quienes construyen y operan sistemas agénticos en la práctica — vibe coding, el agente ejecuta. La tercera es la traducción del método para cuando el código lo escribe el humano y el modelo se consulta puntualmente, no ejecuta solo. Las capas se necesitan entre sí — una sin las otras produce o burocracia sin ejecución, o ejecución sin criterio, o disciplina que solo sirve si hay un agente actuando.

## Contenido

- [`01-marco-agentificacion-empresarial.md`](./01-marco-agentificacion-empresarial.md) — **Capa I.** Para equipos directivos, CTOs y quienes deciden si una empresa agentifica y cómo lo hace. Secuencia de 7 pasos (Paso 0 a Paso 6), de la condición de entrada al protocolo de rollback.
- [`02-framework-ar-practitioners.md`](./02-framework-ar-practitioners.md) — **Capa II.** Para ingenieros, developers y practitioners que construyen y operan sistemas agénticos con vibe coding (el agente ejecuta). Deuda técnica agéntica, los patrones del Framework AR (v1 a v3), el Ciclo AR, cuándo NO usar un agente, y el estado del arte.
- [`03-metodo-ar-desarrollo-manual.md`](./03-metodo-ar-desarrollo-manual.md) — **Capa III.** Para cuando el código lo escribís vos y el modelo se consulta, no ejecuta. Mismo Ciclo AR con los roles invertidos, y qué patrones de la Capa II aplican directo, cuáles se traducen y cuáles no.

## Qué archivo se lleva un proyecto nuevo

- **Si el proyecto va a ser vibe-codeado** (el agente escribe el código): copiá [`reglas-para-el-agente.md`](./reglas-para-el-agente.md) dentro del proyecto — está escrito para pegarse en el `CLAUDE.md` (o importarse con `@ruta/reglas-para-el-agente.md`), le habla al modelo directamente. [`ciclo-ar-bolsillo.md`](./ciclo-ar-bolsillo.md) es el complemento para vos: lo tenés a mano para armar el plan antes de abrir el chat, no se le pega al agente.
- **Si vas a programar vos, consultando al modelo puntualmente:** usá [`03-metodo-ar-desarrollo-manual.md`](./03-metodo-ar-desarrollo-manual.md) — es para vos, no para pegarle a nadie.

## Versionado

El contenido vive en un único set de archivos siempre vigente — no hay carpetas por versión. Las versiones se marcan con **git tags** (`v1.0`, `v2.0`...) sobre el commit exacto, y el detalle de qué cambió y por qué queda en [`CHANGELOG.md`](./CHANGELOG.md). Ver ahí el historial completo.

## Licencia

Pendiente de definir antes de publicar el repositorio.
