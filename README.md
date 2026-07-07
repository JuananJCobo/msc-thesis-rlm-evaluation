# Evaluación experimental de Recursive Language Models para el análisis automatizado de literatura científica

Trabajo de Fin de Máster - Máster Universitario en Inteligencia Artificial - Universidad Tecnológica Atlántico-Mediterráneo - Curso 2025/2026

**Autor:** Juan Antonio Jiménez Cobo

**Director:** Pablo Manuel Berná Larrosa

---

## Descripción

Este repositorio contiene el código, datos y resultados del componente práctico del Trabajo de Fin de Máster, el cual consiste en el diseño e implementació de un sistema de evaluación experimental de tres sistemas para tareas de procesamiento de contexto largo largo aplicadas al análisis de literatura científica. Los sistemas evaluados son:

- **Large Language Models (LLM)** - Se implementan mediante llamadas directas a la API. Procesan el contexto completo en cada llamada.
- **Retrieval Augmented Generation (RAG)** - Implementado con LlamaIndex y ChromaDB como almacén vectorial, ajustado con los parámetros `top_k=5, chunk_size=512`.
- **Recursive Language Models (RLM)** - Metodología propuesta por Zhang et al. (2025).

Cada sistema fue implementado utilizando dos modelos de lenguaje: GPT-5-4 mini y Gemini 2.5 Flash. En el caso de los RLM, se emplearon GPT-5.4 nano y Gemini 2.5 Flash-Lite como modelos para las sub-llamadas recursivas.

## Diseño experimental

El sistema experimental cuenta con las siguientes características:

- Un corpus de 55 artículos académicos sobre el comportamiento estratégico de LLM en entornos de teoría de juegos, construido mediante una Revisión Sistemática de Literatura siguiendo el protocolo PRISMA.
- 4 subconjuntos del corpus con tamaño creciente: C1 (~210.000 tokens), C2 (~280.000 tokens), C3 (~360.000 tokens), C4 (~520.000 tokens).
- 40 consultas con sus respectivas respuestas de referencia anotadas manualmente y divididas en 3 niveles de complejidad:
  - Extracción factual (16 consultas): Requieren extraer un dato específico del contexto
  - Comparación (14 consultas): Requieren identificar dos artículos del corpus y comparar las diferencias entre cada enfoque
  - Síntesis (10 consultas): Requieren identificar patrones comunes entre todos los registros del corpus, agregarlos y sintetizar la información.

- Cada ejecución fue repetida 2 veces para obtener resultados más robustos desde un punto de vista estadístico. El número total de ejecuciones realizadas fue de 1.760 ejecuciones.
- Para la evaluación de las respuestas se empleó la metodología *LLM-as-judge*, en donde un LLM juez (GPT-5.4 mini) evaluó la calidad de las respuestas, comparándolas con las respuestas de referencia y asignándoles una puntuación en la escala discreta 1-5.

## Resultados principales

- Los LLM base obtienen el mayor rendimiento global en todos los tipos de consultas, sin mostrar degradación a medida que la longitud del contexto aumenta.
- RLM GPT-5.4 mini permite aumentar considerablemente la cantidad de contexto procesado por el LLM base, el cual cuenta con una ventana de contexto de 272.000 tokens. La ventana de contexto de Gemini 2.5 Flash es de 1 millón de tokens, luego RLM no muestra una mejora en la escala de los experimentos (el contexto total es de 520.000 tokens)
- RLM muestran un potencial en tareas de comparación de síntesis, obteniendo resultados similares a LLM base y superiores a RAG. No obstante, su rendimiento se ve limitado por 3 patrones de fallo:
  1. Errores de saturación de la API que no fueron detectados por el pipeline de experimentación.
  2. Alucinaciones del modelo de sub-llamadas Gemini 2.5 Flash-Lite.
  3. Fallos de interacción con el entorno REPL por parte de RLM GPT-5.4 mini.
- El análisis coste-calidad sitúa a RLM GPT-5.4 mini en la frontera de Pareto al excluir los fallos de interacción con el REPL.
- Un experimento de ablación para ajustar el prompt raíz redujo en un 38,81% el número de ejecucuiones de RLM GPT-5.4 mini que mostraban fallos de ejecución con el REPL.


## Estructura del repositorio

```
proyect/
├── corpus/                           
│   ├── extraction_report.csv         # Estadísticas de extracción de cada artículo
│   └── preprocessing_report.csv      # Estadísticas del preprocesamiento de cada artículo
├── subsets/                          # Registros de cada subconjunto del corpus
│   ├── subset1_metadata.csv
│   ├── subset2_metadata.csv
│   ├── subset3_metadata.csv
│   └── subset4_metadata.csv
├── docs/
│   └── TFM_Juan_Antonio_Jimenez_Cobo.pdf       # Memoria del trabajo
├── experiments/
│   ├── results/                      # Registros de las ejecuciones de los experimentos
│   ├── rlm_logs/                     # Registros de las trayectorias de razonamiento de los sistemas RLM
│   └── experiment_summary.csv        # Informe de las ejecuciones de los experimentos
├── figures/                          # Figuras empleadas en la memoria
├── notebooks/                        # Libretas de Google Colab con el código fuente del proyecto
│   ├── 01_text_extraction.ipynb      # Pipeline de extracción de texto de los archivos PDF de los registros del corpus
│   ├── 02_preprocessing.ipynb        # Pipeline de preprocesamiento de los textos extraídos
│   └── 03_experiments.ipynb          # Pipeline principal de experimentación 
├── queries/
│   └── queries.json                  # Listado de las consultas empleadas en los experimentos y sus respuestas de referencia
├── slr/                              # Guía para reproducir la revisión Sistemática de Literatura empleada para la creación del corpus
└── README.md
```

## Reproducibilidad

### Requisitos previos

- Python 3.10+
- Cuenta de Google Colab con Google Drive
- Claves de API de [OpenAI](https://platform.openai.com/) y [Google Gemini](https://aistudio.google.com/)

### Instalación

```bash
# Clonar el repositorio
git clone https://github.com/JuananJCobo/msc-thesis-rlm-evaluation
cd msc-thesis-rlm-evaluation

# Instalar dependencias
pip install -r requirements.txt

# Configurar variables de entorno
cp .env.example .env
# Editar .env con tus claves de API
```

### Ejecución

Los notebooks están diseñados para ejecutarse en Google Colab con Google Drive montado. Ejecuta los notebooks en el siguiente orden:

| Notebook | Descripción |
|---|---|
| `01_text_extraction.ipynb` | Extracción y preprocesamiento del corpus desde PDF |
| `02_query_design.ipynb` | Diseño y anotación manual de consultas |
| `03_experiments.ipynb` | Ejecución de los experimentos (LLM base, RAG, RLM) |

> [!NOTE]
> La ejecución completa del experimento requiere acceso a las APIs de OpenAI y Google Gemini y puede incurrir en costes de API. Los resultados completos están disponibles en `experiments/` para reproducir únicamente el análisis sin necesidad de reejecutar los experimentos.

## Referencias

Zhang, A. L., Kraska, T., & Khattab, O. (2026). *Recursive Language Models*. arXiv:2512.24601. https://arxiv.org/abs/2512.24601

Repositorio oficial de la biblioteca RLM:
https://github.com/alexzhang13/rlm

## Licencia

- El código de este repositorio está bajo licencia [MIT](LICENSE).

- La memoria del TFM (`docs/memoria.pdf`) está bajo licencia 
[CC BY-NC-ND 4.0](https://creativecommons.org/licenses/by-nc-nd/4.0/). Se permite compartir con atribución, sin uso comercial y sin modificaciones.
