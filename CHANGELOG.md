# Changelog — Método AR

Versionado por tags de git (`v1.0`, `v2.0`, ...), no por carpetas — el contenido vive en un único set de archivos siempre vigente. Este archivo documenta qué cambió entre versiones y por qué.

## v3.0 — sin publicar

**Qué cambió:** se agregó la sección `09 — Patrones y Riesgos v3` a `02-framework-ar-practitioners.md`, con 5 patrones nuevos y 2 riesgos observados sin patrón resuelto todavía. `ciclo-ar-bolsillo.md` y `reglas-para-el-agente.md` se actualizaron con las versiones operativas de estos patrones. Se agregó además `03-metodo-ar-desarrollo-manual.md` (Capa III), una traducción del método para cuando el código lo escribe el humano y el modelo se consulta puntualmente — las Capas I y II asumen vibe coding (el agente ejecuta); la Capa III no.

**Por qué — origen de cada patrón (trazabilidad por proyecto):**

| Patrón/Riesgo | Proyecto que lo levantó | Evidencia concreta |
|---|---|---|
| P-09 — Gradiente de Decisión Propia | [Siwar](../siwwar/siwar-app) | `AVANCE_DISENO.md`: decenas de anotaciones "decisión propia" sin distinguir peso — desde reusar un almacén existente hasta reordenar el currículo del curso |
| P-10 — Decisión Propia Pre-Acordada | [Siwar](../siwwar/siwar-app) | `AVANCE_DISENO.md` línea 1106: "decisión propia acordada con Luis" — acordada antes de codear, no reportada después |
| P-11 — Bitácora de Reversión | [Helecho](../Helecho) | `funcionalidades2.md`: "⛔ Intento revertido" del subrayado por coordenadas, documentado con el mismo detalle que una función viva |
| P-12 — Secretos Fuera del Contexto | [Helecho](../Helecho) | `estado_sesion_9jul.md`: un token de GitHub se pegó sin querer en el chat; se revocó igual aunque no se hubiera usado |
| P-13 — Convención de Nombres de Archivo | Siwar **y** Helecho (comparación) | Helecho mezcla `apuntesV1/` con `apuntes_v2/`, y `estado_sesion_9jul.md` ordena mal contra `estado_sesion_11jul.md`; Siwar usa fechas ISO completas en las notas fechadas pero `AVANCE_DISENO.md`/`LIBRERIAS.md` en otro estilo — ningún proyecto define la convención una sola vez |
| R-01 — Síntoma que sobrevive al reset | [Helecho](../Helecho) | Bug del ícono del AppImage: dos causas encadenadas descubiertas en sesiones distintas (10 y 11 jul), una tercera causa relacionada en una sesión posterior |
| R-02 — Densidad de decisión propia sin agregación | [Siwar](../siwwar/siwar-app) | Observación derivada de la densidad de "decisión propia" en `AVANCE_DISENO.md` — no se detectó como incidente real, pero el framework tampoco tiene cómo detectarlo si pasara |

**Nada de v1.0 ni v2.0 se modificó ni se reescribió** — v3 es aditivo, sección nueva al final del documento, consistente con P-06 (append-only con ancla estable) aplicado a este mismo repositorio.

## v2.0 — sin publicar

**Qué cambió:** se agregó la sección `08 — Patrones Emergentes (v2)` a `02-framework-ar-practitioners.md`, con 4 patrones nuevos: P-01b (Arquitectura de Información por Audiencia), P-06 (Anclas Estables de Versionado), P-07 (Case Study de Desviación), P-08 (Alcance Explícito del Bloque).

**Por qué:** los 5 patrones originales se validaron en proyectos cortos. Aplicar el Ciclo AR completo a un proyecto de varias semanas (Helecho) expuso 4 límites: un solo `.md` no escala cuando el proyecto acumula estado/historia/planes/sesiones; un documento que crece necesita anclas estables para no romper referencias cruzadas; una desviación de varias rondas necesita postmortem, no solo medición; y un plan aprobado necesita declarar su límite explícito, no solo su alcance.

**Nada de v1.0 se modificó ni se reescribió** — v2 es aditivo, sección nueva al final del documento, consistente con P-06 (append-only con ancla estable) aplicado a este mismo repositorio.

## v1.0 — mayo 2026

Versión original. Dos capas: `01-marco-agentificacion-empresarial.md` (Capa I, Paso 0–6) y `02-framework-ar-practitioners.md` (Capa II: deuda técnica agéntica, 5 patrones, Ciclo AR, cuándo NO usar un agente, conceptos aplicados, estado del arte, el diferencial).
