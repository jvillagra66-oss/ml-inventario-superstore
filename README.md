eadme_content = """# Proyecto de Ciencia de Datos & Machine Learning: Análisis e Inventario Superstore

Este repositorio contiene el flujo de trabajo completo para el análisis de transacciones, segmentación de clientes y predicción del riesgo de desabastecimiento (*Stockout Risk*) utilizando un dataset de **Kaggle** de una tienda minorista (*Superstore*).

## 📋 Tabla de Contenidos
1. [Descripción del Proyecto](#descripción-del-proyecto)
2. [Análisis Exploratorio de Datos (EDA)](#análisis-exploratorio-de-datos-eda)
3. [Preprocesamiento y Estandarización](#preprocesamiento-y-estandarización)
4. [Modelado de Clasificación (Riesgo de Stockout)](#modelado-de-clasificación-riesgo-de-stockout)
5. [Evaluación y Control de Sobreajuste (Overfitting)](#evaluación-y-control-de-sobreajuste-overfitting)
6. [Segmentación de Clientes (Clustering K-Means)](#segmentación-de-clientes-clustering-k-means)
7. [Resultados y Conclusiones](#resultados-y-conclusiones)

---

## 1. Descripción del Proyecto
El objetivo principal de este proyecto es ayudar a la toma de decisiones de negocio optimizando el control del inventario y comprendiendo el comportamiento financiero de la tienda. Para ello:
- Se predice si una transacción tiene **Riesgo de Quiebre de Stock (Stockout Risk)** (definido cuando la cantidad demandada de productos es mayor a 3).
- Se segmentan las transacciones en grupos para diseñar estrategias personalizadas de abastecimiento.

---

## 2. Análisis Exploratorio de Datos (EDA)
- **Análisis de Nulos y Duplicados**: Se detectaron y eliminaron 17 registros 100% duplicados. El conjunto de datos no presenta valores faltantes.
- **Distribución de Ventas**: La variable `Sales` muestra un fuerte sesgo a la derecha, con la gran mayoría de las transacciones concentradas en montos bajos y algunas ventas atípicas de gran volumen.
- **Correlación**: Existe una correlación moderada entre las Ventas (`Sales`) y las Ganancias (`Profit`) de aproximadamente **0.48**.

---

## 3. Preprocesamiento y Estandarización
Para asegurar la robustez de los algoritmos y evitar fuga de datos (*Data Leakage*), se construyó un pipeline estructurado:
1. **Imputación**: Uso de mediana mediante `SimpleImputer` para prevenir valores nulos.
2. **Escalado**: Aplicación de `StandardScaler` o `MinMaxScaler` en variables numéricas continuas (`Sales`, `Profit`, `Discount`).
3. **Codificación de Categorías**: Uso de One-Hot Encoding (`get_dummies`) para variables clave como el método de envío (`Ship Mode`), región (`Region`) y categoría de producto (`Category`).

---

## 4. Modelado de Clasificación (Riesgo de Stockout)
Se entrenaron y compararon múltiples modelos de Machine Learning para clasificar el riesgo de stockout:

* **Regresión Logística (Línea Base)**: Logró un Accuracy aproximado de **62.5%** en test. Al ajustar el umbral de decisión a un nivel más sensible (47%), se logró mejorar la identificación de situaciones críticas.
* **K-Neighbors Classifier (KNN)**: Evaluado con $K=5$, alcanzando un Accuracy global de **66%**.
* **Árbol de Decisión**: Se implementó una versión podada (`max_depth=3`) y una versión completa para el diagnóstico de la robustez.
* **Random Forest (Modelo Óptimo)**: Mediante una búsqueda en grilla interactiva con `GridSearchCV` (evaluando `n_estimators` e hiperparámetros), se determinó que la mejor configuración es un Random Forest con `max_depth=20` y `100` estimadores, alcanzando una exactitud final en test de **74.0%**.

---

## 5. Evaluación y Control de Sobreajuste (Overfitting)
- **Diagnóstico por Permutaciones**: Se calculó la importancia de variables por permutación comparando el conjunto de entrenamiento contra el de prueba (*Train vs Test Set*). Se comprobó que `Sales` y `Profit` son las variables con mayor peso predictivo, manteniendo una excelente capacidad de generalización en datos no vistos.
- **Árbol de Decisión Podado vs Completo**:
  - El árbol sin límite de profundidad memorizó el dataset de entrenamiento (100% Accuracy) pero cayó en sobreajuste.
  - El árbol podado (`max_depth=3`) estabilizó la exactitud en un **65.1%** tanto en Train como en Test, demostrando un comportamiento perfectamente equilibrado e interpretable.

---

## 6. Segmentación de Clientes (Clustering K-Means)
Utilizando únicamente las variables financieras de `Sales` y `Profit`, se evaluaron soluciones de agrupamiento de $K=2$ a $K=10$:
- **Método del Codo y Coeficiente de Silhouette**: Señalaron una estructura óptima de segmentación.
- **Clustering Final con K=5**: El análisis de perfiles reveló la existencia de:
  - **Clústeres de alta frecuencia / bajo valor**: Transacciones comunes con bajo riesgo individual.
  - **Clústeres de alto valor y alta rentabilidad**: Grupos que representan el núcleo premium de facturación.
  - **Clúster de pérdidas críticas**: Transacciones de alto volumen pero con retornos altamente negativos, las cuales presentan la tasa más elevada de riesgo de stockout (**92.3%**).

---

## 7. Resultados y Conclusiones
1. **Pipeline Robusto**: El uso de GridSearchCV permitió encontrar un modelo robusto que predice con precisión el comportamiento del stockout.
2. **Importancia Financiera**: El volumen de ventas es el indicador más crítico para anticipar desabastecimientos de stock.
3. **Acción de Negocio**: Se aconseja priorizar el stock de seguridad en los productos asociados al clúster de alta pérdida financiera y alta rotación para mitigar riesgos operativos.
"""

with open("README.md", "w", encoding="utf-8") as f:
    f.write(readme_content)

print("¡Archivo README.md creado y actualizado con los últimos resultados del proyecto!")
