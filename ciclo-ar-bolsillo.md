# Ciclo AR v2 — de bolsillo
> Copiar y pegar al inicio de cualquier proyecto. Versión completa: `02-framework-ar-practitioners.md`.

---

## PREMISA
Un modelo no piensa. Responde según el contexto que le construyes.
Tu trabajo no es explicarle la tarea — es construir el contexto correcto.

---

## PASO 1 — PLANEAR
Antes de abrir el chat, prepara:
- Un `.md` con el contexto del proyecto (stack, estructura, convenciones) — máximo 150 líneas.
- **Si el proyecto va a durar semanas** (no una tarea de un día): no metas todo en ese único `.md`. Separalo por audiencia — un índice de navegación, un estado (qué está hecho / qué falta), una bitácora acumulativa de decisiones, y un plan por bloque de trabajo. Cada documento comprime para un lector distinto.
- La tarea descompuesta en pasos pequeños y ordenados.
- **Qué NO entra en este bloque** — explícito, al lado de qué sí entra. Sin esto el agente "mejora" cosas fuera de alcance y no es un fallo de plan, es un fallo de límite.
- Si hubo sesiones anteriores: un resumen de qué funcionó y qué falló.

**No abras el agente sin esto listo.**

---

## PASO 2 — EJECUTAR
Al darle cada tarea al agente, indícale que al terminar cada paso debe reportar:
- Qué archivos tocó y por qué.
- Qué errores encontró.
- Si resolvió algo de forma diferente a lo que se le pidió — y cómo.

---

## PASO 3 — AUDITAR
Al final de la sesión o de un bloque de tareas, pregúntale:
- ¿Cuánto se desvió del plan original?
- ¿Por qué se desvió?
- ¿Qué decisiones tomó solo que no estaban en el plan?

Guarda esa respuesta. Es tu trazabilidad.
**Si la guardas en una bitácora que va a seguir creciendo:** dale un ancla estable (§1, §2, §3...) y agrega — no reescribas el documento entero cada vez. Así otros documentos pueden referenciar ese punto exacto sin romperse después.

---

## PASO 4 — DETECTAR
Señal de alerta: **dos iteraciones para resolver lo mismo.**

Si el agente intenta resolver algo, falla, y en el siguiente intento vuelve a fallar diferente — el contexto está contaminado de errores. No sigas. Para.

**Si la señal se disparó por un bug real (no solo por desvío de alcance):** no cierres con "se resolvió". Abre un case study corto: qué se probó en cada ronda, por qué falló, cuál fue la causa raíz, y qué lección queda para no repetir el patrón. Vale más la lección que el fix.

---

## PASO 5 — RESETEAR Y REPLANEAR
Abre un chat nuevo. No copies el historial de errores.
Solo lleva:
- Lo que funcionó.
- Lo que falló (limpio, sin el hilo de intentos — o el case study del PASO 4 si aplica).
- El plan ajustado con lo que aprendiste.

El nuevo chat arranca con criterio, no con ruido.

---

> Construido desde Socorro, Santander 🇨🇴
