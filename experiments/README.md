# Experimentos del sistema
Este directorio contiene los registros de las ejecuciones generados durante la fase experimental del trabajo.

## Estructura del directorio
```
experiments/
├── results/                  # Registros JSON de las 1760 ejecuciones totales del sistema
├── rlm_logs                  # Trayectorias de razonamiento de los RLM en formato JSONL
└── experiment_summary.csv    # Informe de los resultados de cada ejecución
```

## experiment_summary.csv
Este documento contiene los resultados de todas las ejecuciones válidas del sistema. Cada fila corresponde a una ejecución individual. El archivo contiene los siguientes campos:

| Campo | Descripción |
|---|---|
| `subset` | Subconjunto del corpus: C1, C2, C3, C4 |
| `system` | Sistema experimental: baseline (LLM base), rag, rlm |
| `model_tag` | LLM del sistema: gemini (Gemini 2.5 Flash), gpt (GPT-5.4 mini) |
| `query_id` | ID de la consulta (ej. 'Q01') |
| `level` | Nivel de complejidad de la consulta: factual, comparison, synthesis |
| `rep` | Número de repetición: 1, 2 |
| `status` | Estado de la repetición (todas son válidas, por lo que tienen el valor 'OK') |
| `latency_s` | Latencia en segundos de la ejecución |
| `cost_usd` | Coste en USD de la ejecución |
| `judge_score` | Puntuación asignada por el juez LLM (escala 1-5) |
| `n_iterations` | Número de iteraciones del bucle de razonamiento de RLM |

## results/
Contiene archivos JSON con el resgistro de las 1.760 ejecuciones totales del sistema experimental, un archivo por ejecución. El nombre del archivo contiene el siguiente formato: `{subset}{system}{model_tag}_{query_id}_rep{rep}.json`. Cada documento JSON contiene los siguientes campos:

| Campo | Descripción |
|---|---|
| `status` | Estado de la ejecución: `OK`, `SKIPPED_CONTEXT_LIMIT`, `ERROR` |
| `subset` | Subconjunto del corpus: `C1`, `C2`, `C3`, `C4` |
| `system` | Sistema evaluado: `baseline`, `rag`, `rlm` |
| `model` | Modelo de lenguaje completo (ej. `gpt-5.4-mini`) |
| `model_tag` | Etiqueta corta del modelo: `gpt`, `gemini` |
| `query_id` | Identificador de la consulta (ej. `Q01`) |
| `level` | Nivel de complejidad: `factual`, `comparison`, `synthesis` |
| `rep` | Número de repetición (1, 2 o 3) |
| `timestamp` | Fecha y hora de la ejecución |
| `response` | Respuesta generada por el sistema |
| `latency_s` | Latencia en segundos |
| `input_tokens` | Tokens de entrada consumidos |
| `output_tokens` | Tokens de salida generados |
| `cost_usd` | Coste en USD de la ejecución |
| `judge_score` | Puntuación asignada por el juez LLM (escala 1-5) |
| `judge_justification` | Justificación del juez para la puntuación asignada |
| `judge_cost_usd` | Coste en USD de la llamada al juez LLM |
| `total_cost_accumulated_usd` | Coste acumulado total hasta esa ejecución |


## rlm_logs/

Contiene las trayectorias de razonamiento completas de los sistemas RLM en formato JSONL generadas por la calse `RLMLogger` de la biblioteca `rlm` de Zhang et al., (2025), organizadas por subconjunto y modelo:
```
rlm_logs/
├── C1_gemini/    # Trayectorias RLM Gemini 2.5 Flash sobre C1
├── C1_gpt/       # Trayectorias RLM GPT-5.4 mini sobre C1
├── C2_gemini/
├── C2_gpt/
├── C3_gemini/
├── C3_gpt/
├── C4_gemini/
└── C4_gpt/

### Visualizador de trayectorias RLM

Las trayectorias de los registros de `experiments/rlm_logs/` se pueden inspeccionar en el visualizador de trayectorias RLM creado por Zhang et al. Para llevarlo a cabo, sigue los siguientes pasos:

```bash
# Clonar la biblioteca RLM
git clone https://github.com/alexzhang13/rlm
cd rlm/visualizer

# Instalar dependencias
npm install

# Lanzar el visualizador (accesible en localhost:3001)
npm run dev
```

Finalmente, abre `http://localhost:3001` en el navegador y carga los archivos JSONL de `experiments/rlm_logs/`.
