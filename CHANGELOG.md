# Changelog — Método AR

Versionado por tags de git (`v1.0`, `v2.0`, ...), no por carpetas — el contenido vive en un único set de archivos siempre vigente. Este archivo documenta qué cambió entre versiones y por qué.

## v2.0 — sin publicar

**Qué cambió:** se agregó la sección `08 — Patrones Emergentes (v2)` a `02-framework-ar-practitioners.md`, con 4 patrones nuevos: P-01b (Arquitectura de Información por Audiencia), P-06 (Anclas Estables de Versionado), P-07 (Case Study de Desviación), P-08 (Alcance Explícito del Bloque).

**Por qué:** los 5 patrones originales se validaron en proyectos cortos. Aplicar el Ciclo AR completo a un proyecto de varias semanas (Helecho) expuso 4 límites: un solo `.md` no escala cuando el proyecto acumula estado/historia/planes/sesiones; un documento que crece necesita anclas estables para no romper referencias cruzadas; una desviación de varias rondas necesita postmortem, no solo medición; y un plan aprobado necesita declarar su límite explícito, no solo su alcance.

**Nada de v1.0 se modificó ni se reescribió** — v2 es aditivo, sección nueva al final del documento, consistente con P-06 (append-only con ancla estable) aplicado a este mismo repositorio.

## v1.0 — mayo 2026

Versión original. Dos capas: `01-marco-agentificacion-empresarial.md` (Capa I, Paso 0–6) y `02-framework-ar-practitioners.md` (Capa II: deuda técnica agéntica, 5 patrones, Ciclo AR, cuándo NO usar un agente, conceptos aplicados, estado del arte, el diferencial).
