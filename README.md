# Proyecto de Ciencia de Datos & Machine Learning: Análisis e Inventario Superstore

Este repositorio contiene el desarrollo metodológico de punta a punta (*End-to-End*) para la analítica avanzada, predicción de riesgos operativos y segmentación estratégica utilizando el dataset transaccional **Superstore**.

A lo largo del proyecto se implementan buenas prácticas de ingeniería de software para ciencia de datos, estructurando flujos reproducibles que transforman datos crudos en modelos predictivos y de segmentación de alto valor para el negocio.

---

## 🚀 Estructura e Hitos del Proyecto

### 1. Carga y Limpieza de Datos
* **Ingesta Automatizada:** Descarga del dataset de forma automática utilizando la API de `kagglehub` sin necesidad de gestionar credenciales manuales.
* **Calidad de Datos:** Identificación y eliminación de registros 100% duplicados (reduciendo el conjunto de datos a 9,977 filas) y confirmación de la ausencia de valores nulos.
* **Depuración:** Eliminación de variables no influyentes para optimizar la eficiencia computacional de los modelos.

### 2. Análisis Exploratorio de Datos (EDA)
* **Análisis de Distribución:** Evaluación del comportamiento de las ventas (`Sales`) y ganancias (`Profit`).
* **Análisis de Correlación:** Mapeo de correlaciones lineales mediante mapas de calor (`seaborn`) para identificar colinealidad y relaciones clave.

### 3. Ingeniería de Características (Feature Engineering)
* **Variable Objetivo Binaria (`Stockout_Risk`):** Creación del target predictivo para identificar transacciones críticas que demandan altos volúmenes de productos (`Quantity > 3`), asociándolas al riesgo operativo de quiebre de stock.
* **Escalado de Datos:** Normalización y estandarización de las variables numéricas financieras continuas usando `MinMaxScaler` y `StandardScaler`.
* **Codificación Categórica:** Transformación robusta de variables cualitativas (`Ship Mode`, `Region`, `Category`) mediante técnicas de *One-Hot Encoding* (`get_dummies` y `OneHotEncoder`).

### 4. Modelado Predictivo Supervisado
* **Regresión Lineal e Interactividad:** Ajuste de modelos numéricos continuos acompañados de simuladores visuales interactivos con `ipywidgets` para entender la relación ventas-ganancias.
* **Clasificación Tradicional (KNN & Regresión Logística):** Análisis detallado de matrices de confusión y calibración del umbral de decisión (reajustado a `0.47`) para mejorar la sensibilidad en la detección del riesgo.
* **Árboles de Decisión:** Análisis empírico del sobreajuste (*Overfitting*) mediante la comparación de un árbol podado (`max_depth=3`) frente a uno completo. También se abordó la clasificación multiclase (3 categorías de productos) evaluada con matrices de confusión de 3x3.
* **Modelos de Ensamble (Random Forest):** Entrenamiento de bosques aleatorios (`RandomForestClassifier`) y análisis de la estabilización del error en función de la cantidad de estimadores.

### 5. Pipelines Automatizados y Optimización
* **Pipelines de Scikit-Learn:** Automatización del flujo de trabajo uniendo etapas de imputación con `SimpleImputer`, escalado con `StandardScaler` y el estimador final.
* **Validación Cruzada Estratificada:** Evaluación estadística del modelo mediante *5-Fold Stratified Cross-Validation* para asegurar la capacidad de generalización.
* **Búsqueda en Grilla (GridSearchCV):** Optimización sistemática de hiperparámetros que determinó que el mejor modelo es un **Random Forest** con `max_depth=20` y `n_estimators=100`, alcanzando una **exactitud final del 74.0%** en el conjunto de prueba.

### 6. Aprendizaje No Supervisado (Segmentación Estratégica)
* **Clustering K-Means:** Agrupación de transacciones basándose puramente en patrones financieros de ventas y ganancias.
* **Selección Matemática de K:** Identificación del número óptimo de segmentos ($k=5$) a través del **Método del Codo (Inercia)** y la métrica del **Coeficiente de Silhouette**.
* **Perfilamiento de Clústeres:** Caracterización operativa de cada uno de los 5 grupos e integración con el análisis supervisado para determinar la tasa real de riesgo de quiebre de stock por segmento (revelando que el Clúster 3 presenta una tasa crítica del **92.3%**).

---

## 🛠️ Requisitos Técnicos

Para reproducir este proyecto, asegúrate de instalar las siguientes dependencias:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn kagglehub ipywidgets
