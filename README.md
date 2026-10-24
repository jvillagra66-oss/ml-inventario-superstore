[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/jvillagra66-oss/ml-inventario-superstore/blob/main/notebooks/01_analisis_inventario.ipynb)

# Proyecto de Ciencia de Datos & Machine Learning: Análisis de Inventario Superstore

Proyecto de ciencia de datos y machine learning sobre el dataset *Sample Superstore* (Kaggle). Cubre el flujo completo: **EDA, limpieza, preprocesamiento, modelado supervisado (clasificación y regresión), aprendizaje no supervisado (clustering K-Means) e interpretación operativa de clústeres**.

## Objetivos
- **EDA y limpieza**: Detección de nulos, duplicados y selección de variables.
- **Preprocesamiento**: Codificación *one-hot*, normalización/estandarización y `train/test split` (80/20).
- **Clasificación (Riesgo de Stockout)**: Regresión Logística, KNN, Árboles de Decisión y Random Forest.
- **Regresión**: Predicción continua de *Sales* con Regresión Lineal.
- **Control de Sobreajuste**: Comparar árbol podado (`max_depth`) vs. árbol completo (*overfitting*).
- **Modelos de Conjunto**: Random Forest y análisis de estabilidad (`n_estimators`).
- **Aprendizaje No Supervisado**: Segmentación de transacciones con K-Means ($K=2$ y $K=5$).
- **Interpretación Ex-Post de Clústeres**: Cruce de clústeres no supervisados con la tasa real de *Riesgo de Stockout (%)*.
- **Interpretabilidad**: Importancia de variables, perfiles de clústeres y prueba de inferencia.
- **Simulador Interactivo**: Interfaz visual con `ipywidgets` para explorar predicciones en tiempo real.

## Dataset
[Sample Superstore (Kaggle)](https://www.kaggle.com/datasets/vivek468/sample-superstore-dataset) — se descarga automáticamente con `kagglehub`, no hace falta subir el CSV.

## Cómo ejecutarlo
1. Clic en el badge **Open in Colab** de arriba.
2. En Colab: *Entorno de ejecución* → *Ejecutar todo*.
3. (Solo la primera vez) `kagglehub` pedirá autorización de Kaggle para bajar el dataset.

### Alternativa local:
```bash
pip install -r requirements.txt
jupyter notebook notebooks/01_analisis_inventario.ipynb

Contenido del NotebookSecciónQué hace1. EDA y LimpiezaShape, tipos, nulos, duplicados, eliminación de columnas redundantes2. PreprocesamientoVariables categóricas, one-hot, normalización y estandarización3. ClasificaciónRegresión Logística y KNN para estimar el riesgo de stockout4. Regresión LinealPredicción continua de Sales y evaluación de errores5. Simulador InteractivoWidgets para explorar el comportamiento de los modelos en tiempo real6. Árboles de DecisiónÁrbol podado vs. completo (demostración de overfitting)7. Árbol MulticlaseClasificación en 3 categorías + matriz de confusión 3×38. Random ForestBosque aleatorio + curva de estabilidad (n_estimators)9. Aprendizaje No SupervisadoSegmentación con K-Means ($K=2$ y $K=5$), Método del Codo y Silhouette Score10. Perfiles de ClústeresCaracterización de grupos por promedios de Sales, Profit y volumen11. Evaluación Ex-Post de ClústeresCálculo de la tasa de Riesgo de Stockout (%) por clúster12. Importancia de VariablesAtributos más relevantes y prueba de inferenciaResultados PrincipalesModeloTarea / SubtemaMétrica ClaveRegresión LogísticaClasificación (stockout)Accuracy ≈ 0.61Regresión Logística (umbral 25%)Clasificación (stockout)Accuracy ≈ 0.62KNNClasificación (stockout)Accuracy ≈ 0.66Regresión LinealRegresión (Sales)MAE = 0.00 | $$R^$ = 1.00Árbol Podado (max_depth=3)ClasificaciónAccuracy ≈ 0.65 (TRAIN = TEST)Árbol Completo (sin podar)ClasificaciónTRAIN 1.00 vs TEST 0.70 → OverfittingÁrbol Multiclase (3 clases)ClasificaciónAccuracy ≈ 0.65Random Forest (100 Árboles)ClasificaciónTEST Accuracy ≈ 0.66 (Generalización óptima)K-Means ($K=2$)Aprendizaje No SupervisadoInercia = 12,803.3 | Silhouette Score = 0.958K-Means Final ($K=5$)Segmentación de ClientesCaracterización de 5 perfiles por volumen de Sales y ProfitEvaluación de Clústeres ($K=5$)Análisis de Riesgo Ex-PostTasa porcentual (%) de Stockout Risk por clústerConclusiones clave:El árbol sin podar memoriza el set de entrenamiento (Accuracy 1.00) y generaliza peor: es el ejemplo claro de overfitting frente al árbol podado.Random Forest alcanza una exactitud final de 0.66 en Test, mejorando la estabilidad del árbol individual sin caer en sobreajuste.La segmentación no supervisada mediante K-Means ($K=5$) identificó 5 perfiles operativos diferenciados. El análisis ex-post reveló qué clústeres concentran la mayor tasa de Riesgo de Stockout (%), permitiendo anticipar políticas de inventario según el perfil de la transacción.Dependenciaspandas, numpy, matplotlib, seaborn, scikit-learn, kagglehub, ipywidgets.Estructura del Repositorioml-inventario-superstore/
├── notebooks/
│   └── 01_analisis_inventario.ipynb
├── README.md
├── requirements.txt
└── .gitignore
