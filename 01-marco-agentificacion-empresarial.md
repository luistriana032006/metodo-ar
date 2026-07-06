# Capa I — Marco de Agentificación Empresarial

Para equipos directivos, CTOs y quienes deciden si una empresa agentifica y cómo lo hace. La secuencia importa: saltarse pasos no acelera el proceso — lo fragiliza.

---

## Paso 0 — Condición de Entrada: Documentación con Criterio

Antes de auditar hay una pregunta más fundamental: ¿la empresa tiene sus procesos documentados en algún formato que un agente pueda leer y un ingeniero pueda mantener? Si la respuesta es no, el Paso 0 no es una auditoría — es una construcción desde cero, y eso cambia el alcance y el tiempo del proyecto completo.

> La documentación para agentes no es documentación cualquiera. Debe ser unificada (no fragmentada en 40 archivos que nadie conecta), con criterio (qué incluir y qué no), y versionada con la misma disciplina que el código. Documentación desactualizada es peor que no tener documentación — le da al agente un mapa de un mundo que ya no existe.

**Condición mínima de entrada al Paso 1:** al menos los procesos principales tienen un documento que describe inputs, outputs, responsable, y qué pasa cuando falla. Sin eso, la auditoría del Paso 1 incluye construir esa documentación primero.

> **Regla:** Si el proceso vive solo en la cabeza de alguien, agentificarlo primero requiere verbalizarlo.

---

## Paso 1 — Auditar y Documentar: Antes de Agentificar

No para implementar IA todavía. Para tener un contexto histórico real de la empresa y encontrar vulnerabilidades que ya existen hoy. Algunas se van a agravar con la agentificación. Lo que no se puede parchear fácil debe quedar en un entorno con más autorizaciones.

> **Automatizado no es lo mismo que resuelto.** Un proceso automatizado es un proceso congelado en el estado en que estaba cuando lo automatizaste. La fricción humana que se elimina a veces era la que detectaba que algo ya no tenía sentido.

*Términos: Pre-deployment Risk Assessment · Technical Debt Mapping · Process Audit*

---

## Paso 2 — Clasificar Procesos por Criticidad

No todos los procesos merecen el mismo nivel de automatización. Definir la escala antes de empezar evita que lo urgente desplace lo importante.

| Nivel | Descripción | Acción |
|---|---|---|
| 3 | Automatizable completamente, bajo riesgo | Automatización total |
| 2 | Crítico pero interceptable en otro flujo | Automatización supervisada |
| 1 | Core del negocio — fallo con consecuencias irreversibles | Ojos humanos siempre |

> La clasificación no la define una sola persona. Requiere dos voces obligatorias: el técnico que sabe cómo falla el sistema, y quien entiende cuánto le cuesta a la empresa que falle. Sin las dos, la clasificación es incompleta. Test práctico: si este proceso falla y nadie lo detecta en 24 horas, ¿qué le pasa a la empresa? La respuesta a esa pregunta define el nivel — no la complejidad técnica.

*Términos: Criticality Tiers · Risk Classification · Process Prioritization · Dual-Role Assessment*

---

## Paso 3 — Human-in-the-Loop Proporcional al Riesgo

No todo necesita el mismo nivel de supervisión. Los procesos nivel 1 requieren validación humana antes de ejecutarse. Los nivel 3 corren solos. La supervisión es proporcional al daño potencial, no uniforme.

> El humano en el loop debe ser el experto del dominio que se está automatizando — no un revisor genérico. Si se automatiza una campaña de marketing, el aprobador es quien creó la campaña. Si es una parte del código, el desarrollador que trabaja en ese sector. Un aprobador que no entiende lo que valida convierte la supervisión en teatro de seguridad.

> **Regla:** La supervisión cosmética es peor que no tener supervisión — da falsa sensación de control.

*Términos: Human-in-the-Loop (HITL) · Autonomous vs Supervised Agents · Approval Gates · Domain Expert Review*

---

## Paso 4 — Probar en Entorno Controlado Antes de Producción

Un entorno espejo con acceso completo pero aislado. Se inyectan datos reales, se sobrecarga deliberadamente el sistema y se observa cómo se propagan los errores. Lo que falla en el laboratorio no falla en producción.

> **Regla:** Nunca el primer fallo en producción. Siempre en staging primero.

*Términos: Chaos Engineering · Load Testing · Staging Environment · Fault Injection*

---

## Paso 5 — Monitoreo Continuo en Producción

El mayor riesgo de un sistema agéntico no es el fallo ruidoso — es el fallo silencioso que se propaga en cadena sin que nadie lo detecte a tiempo. El monitoreo debe ser activo, no reactivo.

> Un agente que parece funcionar puede estar tomando decisiones ligeramente incorrectas durante semanas antes de que alguien lo detecte. Para cuando el error es visible, el daño ya está hecho. El monitoreo pasivo no es suficiente.

*Términos: Observability · Agent Monitoring · Circuit Breakers · Fault Propagation Detection*

---

## Paso 6 — Protocolo de Rollback: Qué Hacer Cuando Falla

El marco lleva hasta el monitoreo, pero el ciclo no está completo sin definir qué pasa cuando el circuit breaker dispara. Un sistema agéntico sin protocolo de rollback documentado garantiza caos en el momento más crítico.

| Fase | Acción | Responsable |
|---|---|---|
| Detección | El circuit breaker dispara o el monitor detecta anomalía | Técnico / Monitor |
| Aislamiento | Detener el agente afectado sin detener procesos independientes | Ingeniero |
| Reversión | Volver al proceso manual o a la versión anterior del agente | Técnico + Negocio |
| Diagnóstico | Analizar logs, identificar punto de fallo, estimar impacto real | Técnico + Negocio |
| Decisión | ¿Se corrige y se vuelve a desplegar o se reclasifica el proceso? | Dirección |

> **Regla:** El rollback no es un fracaso — es evidencia de que el sistema de monitoreo funcionó.

*Términos: Rollback Protocol · Incident Response · Graceful Degradation · Manual Fallback*
