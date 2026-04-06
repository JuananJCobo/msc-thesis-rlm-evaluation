# Evaluación experimental de Recursive Language Models para el análisis automatizado de literatura científica

Trabajo de Fin de Máster - Máster Universitario en Inteligencia Artificial - Universidad Tecnológica Atlántico-Mediterráneo - Curso 2025/2026

**Autor:** Juan Antonio Jiménez Cobo

**Director:** Daniel Fernández Fernández

🚧 **Estado en desarrollo** — Fase experimental en curso (abril 2026)

---

## Descripción

Este repositorio contiene el código, metodología, datos y resultados del componente práctico del Trabajo de Fin de Máster, el cual consiste en una evaluación experimental de tres sistemas para tareas de procesamiento largo aplicadas al análisis de literatura científica. Los sistemas evaluados son:

- **Recursive Language Models (RLM)** - Metodología propuesta por Zhang et al., 2025.
- **Large Language Models (LLM)** - LLM tradicionales que se emplean como baseline.
- **Retrieval Augmented Generation (RAG)**

La evaluación se realiza sobre diferentes corpus de artículos académicos, cuyos volúmenes varían de 10 a 25 artículos, empleando un dataset de consultas anotadas manualmente clasificadas en tres niveles de complejidad: extracción factual, comparación metodológica y síntesis e identificación de lagunas.

**Hipótesis inicial:** Se parte desde la premisa de que los RLM ofrecen ganancias significativas en tareas de procesamiento de contexto largo frente a modelos base y alternativas como RAG que justifican su mayor complejidad arquitectónica.

**Objetivo final:** Se espera identificar el umbral en la longitud del contexto a partir del cual los resultados obtenidos por RLM mejoran significativamente al resto de alternativas empleadas, restringiendo el dominio al de literatura científica. Asimismo, se espera identificar limitaciones prácticas de los RLM en las tareas evaluadas.

## Estructura del repositorio

```
data/ → corpus de artículos según su volumen y dataset de consultas anotadas manualmente
src/ →  código fuente para la implementación de los sistemas y métricas empleadas
notebooks/ →  Google Colab Notebooks con el procesamiento de texto crudo, pilotos de experimentos y análisis de resultados
experiments/ →  configuraciones y resultados de los experimentos
outputs/ →  figuras y tablas para su uso en la memoria del trabajo
docs/ →  diario de progreso y protocolo de anotación de las consultas
```

## Reproducibilidad

1. Clona el repositorio
2. Copia `.env.example` como `.env` y añade tus claves de API
3. Instala las dependencias de `requirements.txt`
4. Consulta `docs/experiment_log.md` para ver el estado actual de progreso

## Referencias

Zhang, A. L., et al. (2025). *Recursive Language Models*. arXiv:2512.24601.
https://arxiv.org/abs/2512.24601

Repositorio oficial de la librería RLM:
https://github.com/alexzhang13/rlm
