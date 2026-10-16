# Análisis e Inventario Superstore — Proyecto de Machine Learning

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/jvillagra66-oss/ml-inventario-superstore/blob/main/notebooks/01_analisis_inventario.ipynb)

Proyecto de ciencia de datos y machine learning sobre el dataset *Sample Superstore* (Kaggle). Cubre el flujo completo: **EDA, limpieza, preprocesamiento, modelado supervisado (clasificación y regresión) y control de sobreajuste**.

## Objetivos

- **EDA y limpieza**: detección de nulos, duplicados y selección de variables.
- **Preprocesamiento**: codificación *one-hot*, normalización y `train/test split` (80/20).
- **Clasificación** (riesgo de *stockout*): Regresión Logística, KNN y Árboles de Decisión.
- **Regresión**: predecir *Sales* con Regresión Lineal.
- **Control de sobreajuste**: comparar árbol podado (`max_depth`) vs. árbol completo (overfitting).
- **Modelos de conjunto**: Random Forest y análisis de estabilidad (`n_estimators`).
- **Interpretabilidad**: importancia de variables y prueba de inferencia.
- **Simulador interactivo** con `ipywidgets` para explorar los modelos.

## Dataset

[Sample Superstore (Kaggle)](https://www.kaggle.com/datasets/vivek468/sample-superstore-dataset) — se descarga automáticamente con `kagglehub`, no hace falta subir el CSV.

## Cómo ejecutarlo

1. Clic en el badge **Open in Colab** de arriba.
2. En Colab: *Entorno de ejecución* → *Ejecutar todo*.
3. (Solo la primera vez) `kagglehub` pedirá autorización de Kaggle para bajar el dataset.

Alternativa local:

```bash
pip install -r requirements.txt
jupyter notebook notebooks/01_analisis_inventario.ipynb
```

## Contenido del notebook

| Sección | Qué hace |
|---|---|
| **1. EDA y limpieza** | Shape, tipos, nulos, duplicados, eliminación de columnas |
| **2. Preprocesamiento** | Variables categóricas, *one-hot*, normalización |
| **3. Clasificación** | Regresión Logística y KNN (riesgo de *stockout*) |
| **4. Regresión Lineal** | Predicción de *Sales* |
| **5. Simulador interactivo** | Widgets para explorar el comportamiento de los modelos |
| **6. Árboles de Decisión** | Árbol podado vs. completo (demostración de *overfitting*) |
| **7. Árbol multiclase** | Clasificación en 3 categorías + matriz de confusión 3×3 |
| **8. Random Forest** | Bosque aleatorio + curva de estabilidad (`n_estimators`) |
| **9. Importancia de variables** | Atributos más relevantes y prueba de inferencia |

## Resultados principales

| Modelo | Tarea | Métrica clave |
|---|---|---|
| Regresión Logística | Clasificación (stockout) | accuracy ≈ **0.61** |
| Regresión Logística (umbral ajustado) | Clasificación (stockout) | accuracy ≈ **0.62** |
| KNN | Clasificación (stockout) | accuracy ≈ **0.66** |
| Regresión Lineal | Regresión (Sales) | MAE / R² |
| Árbol podado (`max_depth=3`) | Clasificación | accuracy ≈ **0.65** (TRAIN = TEST) |
| Árbol completo (sin podar) | Clasificación | TRAIN **1.00** vs TEST **0.70** → *overfitting* |
| Árbol multiclase (3 clases) | Clasificación | accuracy ≈ **0.65** |
| Random Forest | Clasificación | evaluación + curva `n_estimators` |

> El árbol **sin podar** memoriza el set de entrenamiento (accuracy 1.00) y generaliza peor: es el ejemplo claro de *overfitting* frente al árbol **podado**.

## Dependencias

`pandas`, `numpy`, `matplotlib`, `seaborn`, `scikit-learn`, `kagglehub`, `ipywidgets`.

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
