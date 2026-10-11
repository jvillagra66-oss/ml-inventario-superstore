# Análisis e Inventario Superstore — Proyecto de Machine Learning

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/jvillagra66-oss/ml-inventario-superstore/blob/main/notebooks/01_analisis_inventario.ipynb)

Proyecto de ciencia de datos y machine learning para el análisis de ventas e inventario de una tienda minorista (dataset *Sample Superstore* de Kaggle). Se entrenan modelos de clasificación y regresión para apoyar la toma de decisiones de negocio.

## Objetivos

- Explorar y limpiar el dataset de transacciones (EDA).
- Detectar **riesgo de quiebre de stock** (stockout) con Regresión Logística y KNN.
- Predecir **ventas (Sales)** con Regresión Lineal.
- Comparar modelos mediante matriz de confusión, accuracy, MAE, MSE y R².
- Simuladores interactivos para explorar el comportamiento de los modelos.

## Dataset

[Sample Superstore (Kaggle)](https://www.kaggle.com/datasets/vivek468/sample-superstore-dataset) — se descarga automáticamente con `kagglehub`, no es necesario subir el CSV.

## Cómo ejecutarlo

1. Hacé clic en el badge **Open in Colab** de arriba.
2. En Colab: *Entorno de ejecución* → *Ejecutar todo*.
3. (Solo la primera vez) `kagglehub` pedirá autorización de Kaggle para bajar el dataset.

Alternativa local:

```bash
pip install -r requirements.txt
jupyter notebook notebooks/01_analisis_inventario.ipynb
```

## Resultados principales

| Modelo | Tarea | Métrica clave |
|---|---|---|
| Regresión Logística | Clasificación (stockout) | accuracy / F1 |
| KNN (K=5) | Clasificación (stockout) | accuracy |
| Regresión Lineal | Regresión (Sales) | R² / MAE / MSE |

> Completar con los valores obtenidos al correr el notebook.

## Estructura

```
ml-inventario-superstore/
├── notebooks/
│   └── 01_analisis_inventario.ipynb
├── README.md
├── requirements.txt
└── .gitignore
```

## Autor

- [jvillagra66-oss](https://github.com/jvillagra66-oss)
