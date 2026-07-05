# Corpus

Este directorio contiene los informes asociados a la extracción de texto y preprocesamiento del corpus de artículos empleados en la fase experimental del TFM, así como los registros que pertenecen a cada subconjunto del corpus (C1, C2, C3 y C4). El listado con los metadatos de los 55 registros analizados puede consultarse en `slr/final/corpus_final_20260415.csv`.

## Estructura del directorio

```
corpus/
├── reports/
│   ├── extraction_report.csv         # Estadísticas de extracción de cada artículo
│   └── preprocessing_report.csv      # Estadísticas del preprocesamiento de cada artículo
├── subsets/                          # Registros de cada subconjunto del corpus
│   ├── subset1_metadata.csv
│   ├── subset2_metadata.csv
│   ├── subset3_metadata.csv
│   └── subset4_metadata.csv         
└── README.md
```

> [!IMPORTANT]
>En el repositorio de trabajo de Google Drive se incluyen adicionalmente las carpetas:
>
>* `corpus/papers/` →  registros descargados en formato .pdf
>* `corpus/raw/` →  archivos .txt con el texto extraído de cada registro
>* `corpus/preprocessed/` →  archivos .json con el texto final preprocesado y algunos metadatos de cada registro
>
>No obstante, no se han incluido en este repositorio por las restricciones de licencia de las editoriales.

## Lista de artículos

Puede encontrarse en la ruta `slr/final/corpus_final_20260415.csv` de este repositorio.

## Limitaciones del preprocesamiento

### Secciones extensas no filtradas automáticamente

El pipeline de procesamiento de los textos de `notebooks/02_preprocessing.ipynb` no consiguió eliminar de forma automática secciones extensas en algunos registros, ya que los enabezados no siguen estructuras estándar:

| Paper ID | Páginas totales | Páginas extra | Secciones no eliminadas |
|---|---|---|---|
| paper_08 | 43 | 33 | Apéndices |
| paper_14 | 45 | 35 | Apéndices |
| paper_17 | 34 | 24 | Apéndices |
| paper_44 | 17 | 7 | Referencias y apéndices |
| paper_52 | 91 | 81 | Material suplementario |

Adicionalmente, en otros registros el pipeline falló al eliminar los bloques iniciales de los registros (título + información de los autores + cabeceras editoriales) u otras secciones algo más reducidas:

| Paper ID | Secciones no eliminadas |
|---|---|
| paper_01 | Bloque inicial |
| paper_15 | Bloque inicial |
| paper_18 | Bloque inicial |
| paper_19 | Bloque inicial |
| paper_25 | Bloque inicial |
| paper_35 | Bloque inicial |
| paper_41 | Referencias y biografías de autores |
| paper_48 | Bloque inicial |

En ambos casos, se editaron manualmente los contenidos de los archivos .json con el texto preprocesado de cada registro para eliminar el contenido adicional no filtrado por el pipeline.

### Abstract eliminado incorrectamente

En los siguientes registros el pipeline eliminó incorrectamente el abstract junto al bloque inicial al no identificar correctamente el inicio de la sección:

* paper_32
* paper_38

En ambos casos se restauró el abstract manualmente empleando el texto extraído crudo disponible en `corpus/raw/`, adaptando su formato a los requerimientos del preprocesado.

### Inclusión de ruido adicional

Además de las secciones de referencias y apéndices que no fueron eliminados por el pipeline, en algunos registros preprocesados no se pudo eliminar con éxito las marcas editoriales y cabeceras en secciones intermedias del artículo. No obstante, representan una parte marginal de la longitud total del artículo, luego se optó por incluirlas y aceptarlas como ruido adicional.
