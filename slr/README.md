# Revisión Sistemática de Literatura

En este documento se explica el procedimiento seguido para la realización de la Revisión Sistemática de Literatura (RSL). El objetivo de esta era el de obtener un corpus de aproximadamente 50 artículos científicos para ser empleado en la fase experimental del Trabajo de Fin de Máster. 

La RSL se ha llevado a cabo siguiendo el procedimiento estándar PRISMA (*Preferred Reporting Items for Systematic Reviews and Meta-Analyses*), que establece una guía de 27 pasos y un diagrama de flujo para garantizar la transparencia, calidad y reproducibilidad del proceso.

> **Nota:** La RSL se llevó a cabo entre los días 6 y 15 de abril de 2026. Téngase esto encuenta a la hora de reproducir los resultados.

<br>

## 1. Pregunta de investigación

Se siguió la herramienta estándar PICO, que establece cuatro componentes para definir la pregunta de innvestigación.

| Componente | Descripción | Aplicación al caso |
|---|---|---|
| **P** (Población) | Datos del dominio o problema específico analizado | Grandes modelos de lenguaje (LLM) actuando como agentes en entornos de teoría de juegos |
| **I** (Intervención) | Objeto de estudio | Participación directa del LLM como jugador en juegos estratégicos |
| **C** (Comparación) | Objeto con el cual se compara la intervención principal | Soluciones teóricas clásicas (equilibrio de Nash u otros conceptos de solución), jugadores humanos y/o otros modelos o baselines de referencia |
| **O** (Resultado) | Medida de evaluación de la intervención | Comportamiento estratégico de los LLM medido mediante métricas cuantitativas |


### Formulación de la pregunta de investigación

¿Son capaces los LLM de tomar decisiones de forma racional en juegos estratégicos, y cómo se comparan dichas decisiones frente a soluciones clásicas, jugadores jumanos y/u otros modelos?

<br>

## 2. Criterios de selección de artículos

**Criterios de inclusión**

| Código | Criterio | Etapa de aplicación
|---|---|---|
| CI-1 | Publicado entre 2022 y 2025 | Búsqueda inicial |
| CI-2 | Artículo de revista o comunicación a congreso con revisión por pares | Búsqueda inicial |
| CI-3 | Texto en inglés | Búsqueda inicial |
| CI-4 | Involucra al menos a un LLM, o agente basado en LLM, como jugador en un juego estratégico | Cribado por título y resumen y por texto completo |
| CI-5 | Incluye comparación con soluciones clásicas, jugadores humanos y/u otros LLM o agentes basados en LLM | Cribado por título y resumen y por texto completo |
| CE-6 | Proporciona resultados cuantitativos sobre el comportamiento del LLM o agente basado en LLM | Cribado por título y resumen y por texto completo |

> **Nota:** Los criterios CI-4 y CI-5 fueron ampliados a posteriori para incluir estudios que emplearan agentes basados en LLM, no únicamente LLM tradicionales, e incluir comparaciones entre modelos, además de comparaciones frente a soluciones clásicas y/o jugadores humanos.


**Criterios de exclusión**

| Código | Criterio | Etapa de aplicación |
|---|---|---|
| CE-1 | No incluye ningún LLM (emplean agentes de aprendizaje por refuerzo u otros agentes) | Cribado por título y resumen y por texto completo |
| CE-2 | El marco de experimento es teórico, mientras que la fase experimental es secundaria o complementaria | Cribado por título y resumen y por texto completo |
| CE-3 | Revisión de literatura sin datos propios | Cribado por título y resumen y por texto completo |
| CE-4 | El juego estratégico no es el objeto central de estudio | Cribado por título y resumen y por texto completo |
| CE-5 | El texto completo no se encuentra disponible | Cribado por texto completo |
| CE-6 | Preprints sin publicación en editorial reconocida o comunicación a congresos sin revisión por pares | Corpus final |

> **Nota:** Los artículos incluidos deben de cumplir todos los criterios de inclusión, mientras que cualquier criterio de exclusión es suficiente para excluirlos. Para pulir los criterios de inclusión y exclusión se empleó el modelo de lenguaje Sonnet 4.6.

<br>


## 3. Búsqueda inicial en bases de datos

### Bases de datos consultadas

| Base de datos | Resultados |
|---|---|
| Scopus | 110 registros |
| Web of Science | 40 registros |

Los registros obtenidos de Scopus se pueden consultar en `search/scopus_raw_20260407.csv`, mientras que los de Web of Science se pueden consultar en `search/wos_raw_20260407.csv`.

### Cadena de búsqueda booleana (empleada en ambas bases de datos)
```
("large language model" OR "LLM" OR "GPT" OR "ChatGPT" OR "Llama" OR "Claude"
OR "Gemini" OR "generative AI" OR "foundation model")
AND
("game theory" OR "strategic game" OR "Nash equilibrium" OR "prisoner's dilemma"
OR "bargaining" OR "auction" OR "repeated game" OR "cooperative game"
OR "mechanism design" OR "strategic interaction")
AND
("agent" OR "player" OR "rationality" OR "decision making"
OR "strategic behavior" OR "equilibrium")
```

### Filtros adicionales aplicados en Scopus
- **Años:** 2022-2025
- **Tipo de documento:** Artículos, Comunicaciones a congresos
- **Tipo de fuente:** Revistas, Actas de congresos
- **Áreas temáticas:** Informática, Matemáticas, Ciencias Sociales
- **Idioma:** Inglés

### Filtros adicionales aplicados en Web of Science
- **Años:** 01/01/2022-31/12/2025
- **Tipo de documento:** Artículos, Comunicaciones a congresos
- **Área de investigación:** Informática, Economía Empresarial
- **Idioma:** Inglés

<br>


## 4. Proceso de cribado

Se utilizó la herramienta de software <a href="https://new.rayyan.ai/">Rayyan</a> para asistir con el proceso de cribado.

### Fase 1: Eliminación de duplicados

- Registros totales antes de la deduplicación: 150 (110 Scopus y 40 WoS)
- Duplicados detectados por Rayyan: 33
- Registros únicos tras la eliminación de duplicados: 117 (se pueden consultar en `screening/corpus_deduplicated_20260408.csv`)

> **Nota:** Pese a que la identificación de duplicados fue realizada completamente mediante Rayyan, la decisión final de qué artículos eliminar residió en el usuario.

### Fase 2: Cribado por título y resumen

- Registros sometidos a cribado por título y resumen: 117
- Registros excluidos: 58
- Registros incluidos: 59 (se pueden consultar en `screening/corpus_title_abstract_20260412.csv`)

> **Nota:** Rayyan no incluyó o excluyó ningún registro automáticamente, todo fue realizado por el usuario. Se empleó el modelo de lenguaje Sonnet 4.6 como asistente adicional en algunas decisiones. Al realizar el cribado con un único revisor, se asumen errores en la clasificación de registros durante esta fase, lo cual se intentó mitigar parcialmente incluyendo citas y referencias de los artículos más relevantes del corpus final.


## Fase 3: Cribado por lectura de texto completo

- Registros sometidos a cribado por lectura de texto completo: 59
- Registros excluidos: 16
- Registros incluidos: 43 (se pueden consultar en `screening/corpus_fulltext_20260414.csv`)

> **Nota:** Durante esta fase se identificó un registro duplicado que no fue detectado por Rayyan previamente.
