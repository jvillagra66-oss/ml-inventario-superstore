 🛒 Proyecto de Machine Learning & Clustering: Superstore

Este repositorio contiene el flujo de trabajo completo para el análisis exploratorio, modelado predictivo de riesgo de stock y segmentación de clientes/operaciones utilizando el conjunto de datos de transacciones de **Superstore**.

---

## 📋 Resumen del Proyecto
El objetivo principal es implementar modelos de **Aprendizaje Supervisado** y **No Supervisado** para optimizar la toma de decisiones comerciales, enfocándose en la prevención de quiebres de inventario (Stockout) y la caracterización del comportamiento financiero de las transacciones.

### 🛠️ Tecnologías y Librerías Utilizadas
* **Manipulación de Datos:** `pandas`, `numpy`
* **Visualización:** `matplotlib`, `seaborn`
* **Modelado Predictivo (ML):** `scikit-learn`
* **Descarga Automática de Datos:** `kagglehub`

---

## 🔄 Fases de Implementación e Hitos Recientes

### 1. Extracción e Ingeniería de Datos (ETL)
* **Ingesta Automatizada:** Configuración con la API de `kagglehub` para descargar de manera segura el dataset *Sample-Supermarket*.
* **Limpieza Extrema:** Identificación y remoción exitosa de registros 100% duplicados, restableciendo los índices de manera continua.
* **Selección de Características:** Eliminación estratégica de dimensiones de alta cardinalidad (IDs de órdenes, nombres de clientes) y variables irrelevantes para prevenir ruido en los modelos.

### 2. Modelado de Clasificación (Riesgo de Quiebre de Stock)
Se construyó una variable binaria objetivo llamada `Stockout_Risk` (donde `1` representa una demanda alta de artículos `Quantity > 3` y `0` representa un comportamiento normal).
* **Regresión Logística:** Evaluación del rendimiento con umbrales por defecto (50%) y calibración personalizada mediante probabilidad predictiva (47%) para ajustar la sensibilidad del negocio.
* **K-Nearest Neighbors (KNN):** Entrenamiento interactivo con ajuste dinámico de vecinos ($K$).
* **Árboles de Decisión:** Demostración práctica de control de sobreajuste comparando un árbol con profundidad máxima libre (Overfitting al 100% en Train) versus un árbol podado (`max_depth=3`).
* **Random Forest:** Ensamble de 100 estimadores analizando su curva de estabilización en precisión.

### 3. Diagnóstico Avanzado de Modelos
* **Permutation Importance:** Implementación de análisis por permutación tanto en el set de Entrenamiento como de Prueba para medir la robustez, estabilidad e impacto real de las variables (`Sales` y `Profit` como las de mayor impacto).

### 4. Segmentación Estratégica (Clustering No Supervisado)
* **Normalización:** Uso de `StandardScaler` en las variables continuas financieras para evitar distorsiones por escalas.
* **Selección de $k$ Óptimo:** Evaluación del método del codo (Inercia) y Coeficiente de Silueta (`Silhouette Score`) determinando **$k=5$** como la agrupación más equilibrada.
* **Perfilado de Clústeres:** 
  * Identificación de grupos de bajo valor, transacciones masivas de alto margen, y operaciones críticas con pérdidas financieras.
  * Cálculo de la **Tasa de Riesgo de Stockout** por grupo, revelando que el clúster de compras corporativas masivas tiene hasta un **92.3%** de probabilidad de quiebre de stock.

### 5. Automatización de Flujos (Pipelines & AutoML)
* **Pipeline Robusto:** Construcción de un objeto `Pipeline` de `scikit-learn` que encadena la imputación mediana (`SimpleImputer`), el escalado (`StandardScaler`) y el modelo clasificador en un único flujo blindado contra fugas de datos (Data Leakage).
* **GridSearchCV:** Búsqueda sistemática del mejor estimador e hiperparámetros óptimos entre algoritmos competidores, logrando una precisión final del **74.0%** en el conjunto de prueba usando `RandomForestClassifier(max_depth=20, n_estimators=100)`.
