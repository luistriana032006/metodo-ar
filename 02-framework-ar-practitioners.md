# Capa II — Framework AR para Practitioners

Para ingenieros, developers y practitioners que construyen y operan sistemas agénticos. Estos patrones no se leyeron en un curso — emergieron de la práctica real de construir Trident-AI, haciendo vibe coding en frontends desconocidos, trabajando con Claude Code. Ninguno fue leído en un curso. Todos tienen nombre técnico que llegó después del descubrimiento.

---

## 01 — Deuda Técnica Agéntica

La deuda técnica clásica se ve venir. La deuda agéntica es invisible hasta que explota — los agentes parecen funcionar, dan outputs, mueven datos. El sistema parece vivo. Por dentro se acumula fragilidad.

1. **Deuda de Observabilidad** — Nadie sabe qué están haciendo exactamente sus agentes en producción. Los logs son fragmentados, los razonamientos son opacos. Cuando algo falla, no sabes dónde ni por qué.
2. **Deuda de Confianza** — Si un agente tomó 10,000 decisiones que nadie revisó y 200 estaban mal, ¿cuándo lo descubres? ¿Cuánto daño ya hizo? Las empresas están firmando cheques en blanco.
3. **Deuda de Diseño de Flujo** — Los agentes se enchufan encima de procesos que ya existían y tampoco estaban bien diseñados. No se rediseña el proceso — se le pone un agente encima. Eso duplica la fragilidad.
4. **Deuda de Dependencia** — Pipelines críticos construidos sobre APIs que pueden cambiar, deprecarse o subir de precio. Nadie tiene SLA sobre el comportamiento del modelo — solo sobre la disponibilidad del endpoint.
5. **Deuda de Skill Humano** — La más larga de pagar. Si durante 2 años un agente hace el análisis, quien supervisaba perdió el músculo para hacerlo solo. Cuando el agente falle, no hay a quién recurrir.

---

## 02 — Los 5 Patrones del Framework AR

Descubiertos en la práctica — construyendo Trident-AI, haciendo vibe coding en frontends desconocidos, trabajando con Claude Code. Ninguno fue leído en un curso. Todos tienen nombre técnico que llegó después del descubrimiento.

### P-01 — Compresión de Contexto Intencional
*"El .md del frontend"*

En lugar de dejar que el agente descubra la estructura leyendo todos los archivos, se le entrega un documento de mapa — 150 líneas en lugar de un proyecto completo. Es más barato, más predecible, y arquitectónicamente más sano porque el agente trabaja con la abstracción correcta, no con el detalle completo.

> **Regla:** No dejes que el agente descubra lo que puede leer en un documento. Crea el documento.

*Nombre técnico: Context compression / Information architecture for agents*

### P-02 — Audit Trail por Iteración
*"Qué hizo, qué tocó, por qué lo tocó"*

En cada iteración, el agente reporta: qué archivos modificó, por qué los modificó, qué errores encontró, y cómo los resolvió — especialmente si la solución fue diferente a la indicada. Esto es un log estructurado de razonamiento, no solo de acciones.

> **Regla:** Sin trazabilidad por iteración no sabes si el agente está construyendo o improvisando.

*Nombre técnico: Structured reasoning audit / Agent provenance tracking*

### P-03 — Detección de Desviación del Plan
*"¿Cuánto se alejó del camino original y por qué?"*

Al final de cada sesión se le pregunta al agente cuánto se desvió del plan original para cumplir la tarea, y por qué. Esa información se lleva a un chat nuevo sin el contexto de errores anteriores, para re-planear con trazabilidad limpia.

> **Regla:** La desviación no documentada se convierte en deuda de contexto que acumula errores.

*Nombre técnico: Plan drift detection / Agentic deviation measurement*

### P-04 — Reset de Contexto con Memoria Selectiva
*"Parar, extraer lo útil, reiniciar"*

Cuando el contexto se contamina con errores acumulados — señal: dos iteraciones para resolver lo mismo — se para la sesión. Se extrae solo lo que funcionó y lo que falló limpiamente, y se inicia un nuevo chat con esa trazabilidad como único contexto.

> **Regla:** Dos iteraciones para el mismo problema = el contexto está contaminado. Para y reinicia.

*Nombre técnico: Context window reset / Selective memory extraction (anti-context rot)*

### P-05 — Versionado del Contexto como Código
*"El .md desactualizado es peor que no tener .md"*

Un documento de contexto que no se actualiza cuando cambia el sistema crea un agente que trabaja con información falsa. El contexto debe versionarse con la misma disciplina que el código.

> **Regla:** Si el sistema cambió y el contexto no, el agente opera en un mundo que ya no existe.

*Nombre técnico: Context versioning / Knowledge base staleness prevention*

---

## 03 — El Ciclo AR: Planear, Ejecutar, Auditar, Detectar, Resetear, Replanear

Los cinco patrones no son independientes. Forman un ciclo de mejora continua aplicado al trabajo agéntico. La mayoría de frameworks hablan de cómo usar agentes. Este ciclo también habla de cuándo parar.

| Paso | Qué significa |
|---|---|
| **PLANEAR** | Definir la tarea. Construir el contexto — no explicar la tarea al agente. |
| **EJECUTAR** | El agente actúa. El audit trail se activa desde la primera iteración. |
| **AUDITAR** | Revisar desviación del plan. Documentar qué funcionó, qué falló. |
| **DETECTAR** | ¿Dos iteraciones para lo mismo? El contexto está contaminado. Señal de parada. |
| **RESETEAR** | Reset con trazabilidad selectiva. Solo lo útil entra al nuevo chat. |
| **REPLANEAR** | Nuevo plan con el conocimiento acumulado. El ciclo sube de calidad. |

> Este no es un ciclo de ejecución — es un ciclo de aprendizaje. Cada reset no es un fracaso. Es el momento donde el conocimiento tácito del dominio se convierte en contexto estructurado para la siguiente iteración. Así se construye criterio sobre áreas que no se dominan de antemano.

---

## 04 — Cuándo NO Usar un Agente

Este capítulo no existe en ningún curso de agentes. Todos enseñan cómo usarlos. Nadie enseña cuándo no. Esa omisión es parte del problema.

**✗ El proceso no está documentado**
Si nadie puede describir el proceso en pasos claros con inputs y outputs definidos, un agente no lo va a clarificar — lo va a ejecutar de forma impredecible. Primero documenta, después agentifica.

**✗ El conocimiento es tácito**
El Tacit Knowledge Gap es el límite real de lo automatizable. Si quien hace el proceso no puede verbalizarlo porque lo tiene tan internalizado que ya es automático, el agente no tiene con qué trabajar. El conocimiento que no puede expresarse no puede transferirse a un agente.

**✗ El fallo tiene consecuencias irreversibles**
Procesos donde un error no se puede deshacer — decisiones legales, transacciones financieras sin reversión, comunicaciones externas críticas — no deben automatizarse completamente hasta tener trazabilidad total y rollback probado.

**✗ La API de turno es el único camino**
Si el agente solo puede funcionar si una API específica existe con ese formato y ese precio, no estás agentificando — estás creando dependencia. Si el día que la API cambia no sabes qué reemplaza qué, el riesgo es mayor que el beneficio.

**✗ No hay nadie que lo mantenga**
Un agente en producción sin un ingeniero que entienda el stack completo es infraestructura crítica sin soporte. El día que falle — y va a fallar — no va a haber a quién llamar.

---

## 05 — Conceptos Aplicados Sin Saber Su Nombre

Estos son conceptos que aparecieron en la práctica antes de conocer su nombre técnico. El patrón primero — el nombre después. Eso es exactamente cómo se construye conocimiento real versus conocimiento consumido.

**Context Rot**
*Detectado como: "El agente se pone lento o empieza a repetir errores después de muchas iteraciones"*
El fenómeno donde el contexto se llena de información irrelevante u obsoleta que degrada el comportamiento del agente. Acuñado en investigación de JPMorgan (arXiv, 2026).

**Plan Drift Detection**
*Detectado como: "¿Cuánto se alejó del camino original y por qué?"*
Métrica que mide la desviación de un agente respecto al plan inicial. Empresas con millones en infraestructura agéntica aún no lo miden formalmente.

**Selective Memory Extraction**
*Detectado como: "Parar, sacar solo lo que funcionó, reiniciar"*
Técnica de gestión de ventana de contexto que preserva trazabilidad útil y descarta ruido de errores acumulados antes de reiniciar una sesión.

**Information Architecture for Agents**
*Detectado como: "Un .md de 150 líneas es más barato que dejar leer todo el frontend"*
Diseño intencional del contexto que recibe el agente. En lugar de exponer todos los artefactos, se construye una representación comprimida y precisa.

**Briefing Engineering**
*Detectado como: "Decirle al agente en cada paso qué hizo, qué tocó y por qué"*
Disciplina emergente (paper arXiv 2025) que codifica la intención humana como artefacto principal del proceso. El brief se vuelve tan crítico como el código.

**Tacit Knowledge Gap**
*Detectado como: "El administrativo no sabe describir lo que hace porque lo tiene tan internalizado que es automático"*
El conocimiento que no puede verbalizarse porque está integrado en décadas de práctica. Es el límite real de lo automatizable — no la complejidad técnica.

---

## 06 — Estado del Arte y el Hueco

Al momento de escribir este documento (mayo 2026), existe trabajo académico y empresarial sobre ingeniería agéntica. Pero ninguno cubre el espacio específico de este framework.

**→ Loosely-Structured Software (HKUST/UMacau, 2026)**
Framework de tres capas: View/Context Engineering, Structure Engineering, Evolution Engineering. Académico, teórico, enfocado en sistemas multi-agente a gran escala.

**→ Structured Agentic SE — SASE (arXiv, 2025)**
Propone dualidad SE4H (para humanos) y SE4A (para agentes). Introduce Briefing Engineering. Roadmap de investigación, sin implementación práctica.

**→ Agentic Engineering — LangChain Blog (2026)**
Modela agentes como miembros de equipo. Enfocado en el ecosistema LangGraph. Orientado a empresas, no a practitioners individuales.

**→ Skele-Code — JPMorgan (arXiv, 2026)**
Introduce el concepto de context rot. Propone notebooks estructurados para expertos de dominio. Muy específico en herramienta.

**→ PROV-AGENT (arXiv, 2025)**
Modelo de proveniencia para trazabilidad de agentes usando W3C PROV y MCP. Técnico, orientado a enterprise compliance.

> **El hueco:** Todo lo existente es académico, teórico, o atado a una herramienta específica. No existe un framework práctico, independiente de herramienta, escrito desde la perspectiva de un practitioner que construye software real con estas limitaciones. Con heurísticos observables — no reglas abstractas. Con criterio sobre cuándo NO usar un agente. Construido desde quien entiende que el agente no piensa sino que responde según contexto.

---

## 07 — El Diferencial

Las academias de agentes están creando consumidores de abstracción: gente que sabe llamar una API pero no sabe qué hay adentro. Eso no es un ingeniero de AI — es un usuario avanzado de una API. La diferencia se hace visible el día que la API cambia.

- ✓ Sabe que debajo de un agente hay un modelo que responde según contexto, no uno que piensa
- ✓ Entiende el problema por debajo de la herramienta — puede migrar cuando la herramienta cambia
- ✓ Diseña el contexto como recurso a gestionar, no la tarea como instrucción a dar
- ✓ Tiene criterio sobre cuándo no usar un agente — lo que ningún curso enseña
- ✓ Construye trazabilidad como hábito, no como feature de observabilidad enterprise
- ✓ Ve los árboles, los grafos, el álgebra lineal debajo de cada herramienta que usa

> No debes depender de una empresa — debes adaptarte a ella. Depender: mi sistema solo funciona si esta API existe, tiene este formato, y cuesta lo mismo que hoy. Adaptarse: entiendo qué problema resuelve esta API — si cambia o desaparece, sé qué buscar, qué reemplaza qué, y cuánto me cuesta migrar.

*Construido desde Socorro, Santander, Colombia — Mayo 2026*

---

## 08 — Patrones Emergentes (v2)

Los 5 patrones de la sección 02 se validaron con la disciplina de proyectos cortos. Aplicar el Ciclo AR completo a un proyecto real de varias semanas — construyendo Helecho, con decenas de features y sesiones que se retoman días después — expuso cuatro límites que los patrones originales no cubrían. Mismo origen que los primeros cinco: el patrón apareció en la práctica, el nombre llegó después.

### P-01b — Arquitectura de Información por Audiencia
*"Un solo .md no escala a un proyecto de semanas"*

P-01 comprime el contexto en un solo documento. Pero un proyecto real acumula estado, historia, planes y sesiones — meter todo en un mapa de 150 líneas lo vuelve incompleto o obsoleto en días. La solución no es abandonar la compresión, es separarla por audiencia: un índice de navegación, un marcador de estado (qué está hecho, qué falta), una bitácora acumulativa de decisiones, snapshots de sesión para retomar, y planes acotados por bloque de trabajo. Cada documento comprime para un lector distinto, no para todos a la vez.

> **Regla:** Un documento que sirve para todo no sirve bien para nada. Separa por audiencia, no por tamaño.

*Nombre técnico: Multi-document information architecture / Audience-based context partitioning*

### P-06 — Anclas Estables de Versionado
*"Agregar con ancla, no reescribir"*

P-05 exige mantener el contexto sincronizado con el sistema. En la práctica, un documento de conocimiento que crece (una bitácora, un historial de features) no se reescribe entero cada vez — se le agregan entradas. Si esas entradas llevan un identificador estable (§23, §27...), otros documentos pueden apuntar a un punto exacto del conocimiento sin duplicar contenido y sin romperse cuando el documento sigue creciendo.

> **Regla:** Versiona agregando con ancla estable, no reescribiendo — así ninguna referencia cruzada queda huérfana.

*Nombre técnico: Append-only versioning with stable anchors / Immutable reference IDs*

### P-07 — Case Study de Desviación
*"Dos hipótesis fallidas seguidas: instrumenta, no adivines"*

P-03 mide cuánto se desvió el agente del plan. Cuando la desviación viene de un bug real que tomó varias rondas de intentos fallidos — la señal de alerta del PASO 4 del Ciclo AR (DETECTAR) — medir "cuánto" no alcanza: hay que registrar el camino completo. Qué se probó, por qué falló cada intento, cómo se llegó a la causa raíz, y qué lección generalizable queda. Se documenta como incidente, no como nota al margen.

> **Regla:** Si se dispara la señal de dos iteraciones, no cierres con "se resolvió" — cierra con rondas + causa raíz + lecciones.

*Nombre técnico: Structured deviation postmortem / Root-cause case study logging*

### P-08 — Alcance Explícito del Bloque
*"Qué NO entra en este bloque"*

La sección 04 decide si automatizar algo o no. Pero dentro de una iniciativa ya aprobada, el agente puede desviarse "mejorando" cosas fuera del alcance acordado sin que eso sea, técnicamente, un fallo de plan (P-03) — es un fallo de límite. Declarar explícitamente qué queda fuera de un bloque de trabajo, al lado del plan, evita que la ejecución se expanda sola.

> **Regla:** Todo plan de bloque necesita su lista de "qué NO entra" al lado de su lista de qué sí.

*Nombre técnico: Explicit scope boundary / Out-of-scope declaration*

### Dónde encajan en el Ciclo AR

| Patrón | Refuerza |
|---|---|
| P-01b | PLANEAR — el contexto se construye distinto según quién lo lee |
| P-06 | AUDITAR / RESETEAR — el conocimiento acumulado queda referenciable sin reescribirse |
| P-07 | DETECTAR — la señal de dos iteraciones cierra con postmortem, no con silencio |
| P-08 | PLANEAR — el plan declara tanto el alcance como su límite |

> Estos cuatro patrones no reemplazan a los cinco originales — los rodean. Aparecen cuando el Ciclo AR deja de aplicarse a una tarea de un día y empieza a aplicarse a un proyecto que vive semanas. La prueba de que un patrón nuevo vale la pena no es la elegancia — es que resolvió una fricción real y quedó evidencia de eso en el trabajo, no solo en la teoría.

*Validado en: [Helecho](../Helecho) — mayo–junio 2026.*

---

## 09 — Patrones y Riesgos v3 (de correr el Ciclo AR en paralelo, en dos proyectos)

Los patrones de la sección 08 salieron de aplicar el Ciclo AR a *un* proyecto largo. Correr dos proyectos completos a la vez —Siwar (app educativa, semanas de julio 2026) y Helecho (editor de escritorio, mayo–julio 2026)— con la misma disciplina expuso algo que un solo proyecto no muestra: cómo se acumulan las decisiones propias sesión tras sesión, y qué pasa cuando la convención de nombres de archivo no se define una vez y se respeta, sino que se reinventa cada vez que se abre un documento nuevo. Cuatro patrones nuevos y dos riesgos observados — riesgos porque no hay todavía una solución probada, solo la señal de que hace falta una.

### P-09 — Gradiente de Decisión Propia
*"No toda decisión propia pesa igual"*

P-02 pide marcar cuándo el agente decidió algo por su cuenta. En la práctica esa etiqueta se usa igual para "reusé el almacén que ya existía en vez de crear uno nuevo" y para "cambié el orden pedagógico del curso". Ambas quedan como "decisión propia" sin distinguirse — y eso es exactamente lo que vuelve difícil, al auditar, saber cuál necesitaba tu visto bueno antes de seguir y cuál era solo ruido de trazabilidad. La etiqueta sola no alcanza: hace falta un segundo eje, el peso.

> **Regla:** Clasificá cada decisión propia en cosmética, técnica-interna o de producto. Solo la de producto necesita parar y preguntar antes de seguir — las otras dos se agrupan y se revisan juntas en el PASO 3 (AUDITAR).

*Nombre técnico: Decision impact tiering / Autonomy-weighted deviation logging*

### P-10 — Decisión Propia Pre-Acordada
*"Proponer y acordar en el momento, no reportar después"*

P-03 asume que la desviación se reporta al cerrar la sesión. En la práctica, para las decisiones de peso medio, ya está pasando algo mejor: se proponen y se acuerdan en el momento ("decisión propia acordada con Luis"), antes de escribir el código — no se reportan como hecho consumado al final. Es una versión más estricta de P-03, que ya se aplica sola sin estar nombrada.

> **Regla:** Si una decisión propia es de peso medio o alto (ver P-09), proponela y esperá el visto bueno antes de codear — no la reportes ya hecha al cierre de sesión.

*Nombre técnico: Synchronous deviation approval / Pre-commit decision gating*

### P-11 — Bitácora de Reversión
*"Lo que se construyó bien y se deshizo también es conocimiento"*

P-07 documenta bugs con causa raíz. Pero hay un caso distinto: una funcionalidad que se construyó *bien*, funcionó, y se deshizo igual porque no encajaba en el producto (ejemplo real: subrayado por coordenadas en Helecho, implementado y revertido a pedido del usuario). Sin registrarlo con el mismo detalle que una feature viva, un agente en una sesión futura puede volver a proponer exactamente lo mismo que ya se descartó, sin saber que ya se intentó.

> **Regla:** Documentá lo revertido con el mismo nivel de detalle que lo que quedó — qué se construyó, por qué no sirvió, qué volvió a su lugar. Un "⛔ Intento revertido" al lado de las funcionalidades vivas, no una nota al margen.

*Nombre técnico: Rejected-implementation log / Negative-result documentation*

### P-12 — Secretos Fuera del Contexto
*"Si tocó el chat, se considera quemado"*

Un token de GitHub se pegó sin querer en el chat durante una sesión de Helecho. Se revocó y se regeneró igual, aunque nunca se hubiera usado con mala intención — la copia quedó en el historial de la conversación, y eso basta para tratarlo como comprometido. El segundo token se cargó directo en `.env` desde el editor, nunca a través del agente.

> **Regla:** Ningún secreto (token, contraseña, clave API) entra al contexto del agente, ni para pegarlo ni para que lo genere. Si uno lo toca por accidente, se rota — se haya usado o no.

*Nombre técnico: Secret hygiene / Context-boundary credential isolation*

### P-13 — Convención de Nombres de Archivo
*"Un rol, un nombre, una fecha que ordena bien"*

Entre Siwar y Helecho —y dentro del mismo Helecho, entre `apuntesV1/` y `apuntes_v2/`— el estilo de nombres cambia sin razón técnica: `estado_sesion_10jul.md` (snake_case, sin año, sin cero a la izquierda) al lado de `2026-07-06-mensajes-de-voz.md` (kebab-case, ISO completo); `funcionalidades.md` que se convierte en `funcionalidades2.md` (número pegado, sin separador, parece un duplicado accidental más que una v2 intencional); `estado_sesion_9jul.md` que en `ls` ordena *después* de `estado_sesion_11jul.md` porque "9" > "1" como texto. Ninguno de estos rompe el proyecto — todos hacen más lento encontrar o entender un documento seis semanas después.

> **Regla:**
> - kebab-case siempre (minúsculas, guiones). Excepción: los nombres que herramientas y humanos reconocen por convención fija (`README.md`, `CHANGELOG.md`, `CLAUDE.md`).
> - Fecha en ISO completo `AAAA-MM-DD`, con ceros — nunca `9jul`, nunca sin año. Si `ls | sort` no da el orden cronológico real, el nombre está mal.
> - Carpetas de versión: `v1/`, `v2/`, `v3/` — un dígito, minúscula, igual en todos los proyectos.
> - La versión no se pega al nombre del archivo (`funcionalidades2.md`); vive **dentro** del archivo con anclas estables (P-06, `§1`, `§2`...). Si el archivo de verdad hay que partirlo, el corte lleva guion explícito (`funcionalidades-v2.md`), nunca un número pegado.
> - Un rol conceptual = un nombre fijo, sin importar qué día se escribe. El snapshot para retomar es siempre `sesion-AAAA-MM-DD.md` con la fecha en que se ESCRIBE, no la fecha que describe — la ambigüedad "sesión de hoy" vs. "prep para mañana" se resuelve en el texto, no en el nombre.
> - Vocabulario mínimo por rol (de P-01b), para no reinventarlo cada proyecto: `README.md` (índice), `sesion-AAAA-MM-DD.md` (snapshot para retomar), `bitacora.md` (histórico con anclas §N), `pasos.md` (checklist vivo, se escribe antes y se tacha después con fecha), `pendientes.md` (cola de verificación humana, distinta de `pasos.md`), `plan-<bloque>.md` (plan acotado, con su lista de qué NO entra), `ideas-futuras.md` (aparcadero).

*Nombre técnico: File naming convention / Chronological-sort-safe identifiers*

---

### Riesgos observados (sin patrón resuelto todavía)

Estos dos no llegan a regla porque no hay todavía una solución validada — son la señal de que hace falta una, anotada para no perderla.

**R-01 — Síntoma que sobrevive al reset**
La regla "dos fallos seguidos = parar e instrumentar" (P-07) funciona *dentro* de una sesión — el caso del botón de DeepSeek en Helecho (3 rondas, causa raíz encontrada al instrumentar en la tercera) es el ejemplo de manual. Pero el bug del ícono del AppImage tuvo dos causas encadenadas descubiertas en sesiones distintas (10 y 11 jul), y una tercera causa relacionada apareció en una sesión posterior todavía. El postmortem de P-07 cierra un incidente puntual; no hay hoy un mecanismo para un síntoma que se cierra, vuelve a abrirse con otra causa, y cruza resets de contexto sin que se note que es "la misma familia de bug".

**R-02 — Densidad de decisión propia sin agregación**
Es la cara de riesgo de P-09: un proyecto puede acumular muchas decisiones propias pequeñas, cada una razonable vista sola, que en conjunto terminan moldeando el producto en una dirección que nadie aprobó como bloque. En Siwar y Helecho no se observó que esto haya pasado — pero tampoco hay ninguna alarma en el framework que lo detectaría si pasara. Falta un mecanismo de agregación (¿cuántas decisiones propias de peso medio se acumularon esta semana?) que hoy no existe.

### Dónde encajan en el Ciclo AR

| Patrón/Riesgo | Refuerza |
|---|---|
| P-09 | AUDITAR — clasifica antes de revisar, no todo pesa igual |
| P-10 | EJECUTAR — la aprobación pasa a ser síncrona para lo que pesa |
| P-11 | RESETEAR — lo descartado también viaja al nuevo chat, no solo lo que quedó |
| P-12 | EJECUTAR — límite duro del contexto, no depende del criterio del agente |
| P-13 | PLANEAR — el documento de contexto empieza por tener un nombre que se entiende sin abrirlo |
| R-01 | DETECTAR — el límite de una sesión no es el límite del síntoma |
| R-02 | AUDITAR — falta agregación, no solo etiqueta individual |

*Validado en: [Siwar](../siwwar/siwar-app) (julio 2026) y [Helecho](../Helecho) (junio–julio 2026).*
