# Análisis e Inventario Superstore — Proyecto de Machine Learning

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/jvillagra66-oss/ml-inventario-superstore/blob/main/notebooks/01_analisis_inventario.ipynb)

# Proyecto de Ciencia de Datos & Machine Learning: Análisis de Inventario Superstore

Proyecto de ciencia de datos y machine learning sobre el dataset *Sample Superstore* (Kaggle). Cubre el flujo completo: **EDA, limpieza, preprocesamiento, modelado supervisado (clasificación y regresión), aprendizaje no supervisado (clustering) y control de sobreajuste**.

## Objetivos
- **EDA y limpieza**: Detección de nulos, duplicados y selección de variables.
- **Preprocesamiento**: Codificación *one-hot*, normalización/estandarización y `train/test split` (80/20).
- **Clasificación (Riesgo de Stockout)**: Regresión Logística, KNN, Árboles de Decisión y Random Forest.
- **Regresión**: Predicción de *Sales* con Regresión Lineal.
- **Control de Sobreajuste**: Comparar árbol podado (`max_depth`) vs. árbol completo (*overfitting*).
- **Modelos de Conjunto**: Random Forest y análisis de estabilidad (`n_estimators`).
- **Aprendizaje No Supervisado**: Segmentación del comportamiento de transacciones con K-Means.
- **Interpretabilidad**: Importancia de variables y prueba de inferencia.
- **Simulador Interactivo**: Interfaz visual con `ipywidgets` para explorar predicciones en tiempo real.

## Dataset
[Sample Superstore (Kaggle)](https://www.kaggle.com/datasets/vivek468/sample-superstore-dataset) — se descarga automáticamente con `kagglehub`, no hace falta subir el CSV.

## Cómo ejecutarlo
1. Clic en el badge **Open in Colab** de arriba.
2. En Colab: *Entorno de ejecución* → *Ejecutar todo*.
3. (Solo la primera vez) `kagglehub` pedirá autorización de Kaggle para bajar el dataset.

### Alternativa local:
```bash
├── notebooks/
│   └── 01_analisis_inventario.ipynb
├── README.md
├── requirements.txt
└── .gitignore
pip install -r requirements.txt
jupyter notebook notebooks/01_analisis_inventario.ipynb
