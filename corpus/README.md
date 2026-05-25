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

No obstante, no se han incluido en este repositorio por las restricciones de licencia de las editoriales
