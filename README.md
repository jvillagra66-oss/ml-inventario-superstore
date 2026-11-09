# README.md - Análisis e Inventario Superstore con Machine Learning

Este repositorio contiene el desarrollo completo del análisis exploratorio de datos (EDA), preprocesamiento y modelado predictivo utilizando el conjunto de datos **Sample Superstore**. El objetivo principal es optimizar el inventario mediante la clasificación del **Riesgo de Quiebre de Stock (Stockout Risk)** y el agrupamiento de transacciones comerciales.

---

## 🚀 Resumen del Proyecto y Flujo de Trabajo

### 1. Preparación y Limpieza de Datos
* **Carga de datos:** Descarga automática usando `kagglehub`.
* **Tratamiento de duplicados:** Detección y eliminación de 17 registros idénticos.
* **Ingeniería de variables:**
  * Creación de la variable objetivo binaria `Stockout_Risk` (1 si `Quantity > 3`, de lo contrario 0).
  * Normalización de variables continuas (`Sales`, `Profit`) utilizando `MinMaxScaler` y `StandardScaler`.
  * Codificación de variables categóricas (`Ship Mode`, `Region`, `Category`) mediante One-Hot Encoding.

---

## 📊 Modelos Entrenados y Rendimiento

### A. Modelos Supervisados (Clasificación de Riesgo de Stockout)
Se dividieron los datos utilizando una partición estratificada de **80% Entrenamiento / 20% Prueba** para garantizar la representatividad.

1. **Regresión Logística con Umbrales de Decisión:**
   * **Umbral por defecto (50%):** Accuracy del 61%. Alta precisión para la clase de riesgo (83%), pero bajo recall (10%).
   * **Umbral optimizado (47%):** Incrementó la sensibilidad para detectar situaciones de riesgo, aumentando el recall al 15%.

2. **K-Vecinos Más Cercanos (KNN):**
   * Evaluado con $K=5$ vecinos.
   * **Accuracy Global:** 0.66.

3. **Árbol de Decisión (Control de Sobreajuste):**
   * **Árbol Completo (Sin Podar):** Demostró overfitting extremo con un 100% de exactitud en el set de entrenamiento frente a un 69.6% en test.
   * **Árbol Podado (`max_depth=3`):** Se controló el sobreajuste obteniendo una exactitud equilibrada del **65.1%** tanto en entrenamiento como en pruebas.

4. **Random Forest Classifier (Ensamble):**
   * Se analizó la estabilización del error variando el número de estimadores.
   * Identificación de las variables más influyentes mediante **Importancia por Permutación**, destacando a `Sales` y `Profit` como los factores clave para la clasificación.

---

## 🛠️ Optimización y Automatización (Pipeline & GridSearchCV)

Para consolidar las buenas prácticas en Machine Learning, se implementó un **Pipeline automatizado** integrado por:
1. **Imputación:** Reemplazo de nulos mediante mediana con `SimpleImputer`.
2. **Escalado:** Estandarización con `StandardScaler`.
3. **Clasificador:** Ajuste dinámico de algoritmos.

### Resultados de la Búsqueda en Grilla (GridSearchCV):
Se evaluaron arquitecturas competitivas de Regresión Logística y Random Forest utilizando validación cruzada de 5 pliegues (`cv=5`).

* **Mejor Modelo Seleccionado:** `RandomForestClassifier`
* **Hiperparámetros óptimos:** `max_depth: 20`, `n_estimators: 100`
* **Métricas de Éxito:**
  * **Exactitud promedio en CV (5-fold):** **72.7%**
  * **Exactitud (Accuracy) final en pruebas:** **74.0%**

--- 

## 🎯 Segmentación No Supervisada (K-Means Clustering)

Se aplicó clustering no supervisado en base a `Sales` y `Profit` para perfilar las transacciones comerciales:
* **Evaluación del K Óptimo:** Se analizó el método del codo (Inercia) y el coeficiente de Silhouette, determinando que **$K=5$** proporciona la mejor cohesión y separación de clusters.
* **Perfilamiento de Clústeres:**
  * **Grupo con mayor tasa de Riesgo de Stockout:** El Clúster 3 cuenta con una tasa de riesgo crítica del **92.3%**, asociado a transacciones de alto volumen de ventas con margen negativo.
  * **Grupo con menor tasa de Riesgo:** El Clúster 0 representa transacciones estándar con un **40.6%** de probabilidad de riesgo de quiebre.

---

## 🛠️ Tecnologías Utilizadas
* **Python 3**
* **Pandas / NumPy** (Manipulación de datos)
* **Scikit-Learn** (Pipelines, Modelado, Métricas y Selección de Modelos)
* **Matplotlib / Seaborn** (Visualización interactiva y mapas de calor)
