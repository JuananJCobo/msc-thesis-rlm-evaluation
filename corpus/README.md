# Corpus

Este directorio contiene los informes asociados a la extracción de texto y preprocesamiento del corpus de artículos empleados en la fase experimental del TFM. El listado con los metadatos de los 55 registros analizados puede consultarse en `slr/final/corpus_final_20260415.csv`.

## Estructura del directorio

```
corpus/
├── reports/
│   ├── extraction_report.csv      # Estadísticas de extracción de cada artículo
│   └── preprocessing_report.csv      # Estadísticas del preprocesamiento de cada artículo
└── README.md
```
En el repositorio de trabajo de Google Drive se incluyen adicionalmente las carpetas:

* `corpus/papers/` →  registros descargados en formato .pdf
* `corpus/raw/` →  archivos .txt con el texto extraído de cada registro
* `corpus/preprocessed/` →  archivos .txt con el texto final preprocesado de cada registro

No obstante, no se han incluido en este repositorio por las restricciones de licencia de las editoriales.

## Lista de artículos

Puede encontrarse en la ruta `slr/final/corpus_final_20260415.csv` de este repositorio.

## Limitaciones del preprocesamiento

### Secciones extensas no filtradas automáticamente

El pipeline de procesamiento de los textos de `notebooks/02_preprocessing.ipynb` no consiguió eliminar de forma automática las referencias y apéndices en los siguientes registros, debido a que los encabezados no siguen estructuras estándar:

| Paper ID | Páginas totales | Páginas extra | Secciones no eliminadas |
|---|---|---|---|
| paper_08 | 43 | 33 | Referencias y apéndices |
| paper_14 | 45 | 35 | Referencias y apéndices |
| paper_17 | 34 | 24 | Referencias y apéndices |
| paper_41 | 15 | 2 | Referencias y biografías de autores |
| paper_44 | 17 | 7 | Referencias y apéndices |
| paper_52 | 91 | 81 | Material suplementario |

En estos casos, se editaron manualmente los archivos .txt con el texto preprocesado de cada registro para eliminar el contenido adicional no filtrado por el pipeline.

### Inclusión de ruido adicional

Además de las secciones de referencias y apéndices que no fueron eliminados por el pipeline, en la mayoría de registros preprocesados no se pudo eliminar con éxito las marcas editoriales y cabeceras. No obstante, dado que la proporción de estas partes es mínima con respecto a la totalidad de los artículos, se optó por incluirlas y aceptarlas como ruido adicional.
