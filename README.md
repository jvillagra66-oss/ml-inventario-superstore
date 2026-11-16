  🛒 Superstore Analytics & Predictive Intelligence

![Machine Learning](https://img.shields.io/badge/Machine%20Learning-Supervised-blue?style=for-the-badge&logo=scikit-learn) 
![Python](https://img.shields.io/badge/Python-3.10%2B-green?style=for-the-badge&logo=python) 
![Data Pipeline](https://img.shields.io/badge/Pipeline-End--to--End-orange?style=for-the-badge&logo=git) 

## 📋 Resumen del Proyecto
Este repositorio contiene una solución integral de **Ciencia de Datos y Aprendizaje Supervisado** orientada a la optimización de inventarios y análisis operativo de una cadena minorista (*Superstore*).

El núcleo estratégico del proyecto consiste en predecir y anticipar el **Riesgo de Quiebre de Stock (Stockout Risk)** mediante la modelización de patrones complejos en transacciones financieras de ventas, márgenes de ganancia y descuentos operativos.

---

## 🚀 Arquitectura y Progreso Metodológico

Hemos construido y validado un flujo analítico riguroso estructurado en las siguientes fases técnicas:

### 1. Ingesta e Integración Automatizada
*   Descarga integrada de datasets federados directamente desde la API de **Kaggle** utilizando `kagglehub`.
*   Estandarización de encoding operativo (`Windows-1252`) para preservar la integridad de datos geográficos y comerciales.

### 2. Procesamiento Avanzado de Datos (Feature Engineering)
*   **Estratificación y Limpieza:** Depuración completa de duplicados reduciendo de manera efectiva el ruido de los datos.
*   **Codificación Robusta:** Implementación híbrida de técnicas de codificación (`One-Hot Encoding` / Pandas Dummies) aplicadas a dimensiones logísticas y geográficas críticas como *Ship Mode*, *Region* y *Category*.
*   **Normalización Monetaria:** Ajuste proporcional mediante escalas continuas (`MinMaxScaler` y `StandardScaler`) para homogenizar variables de alta dispersión (*Sales* y *Profit*).

### 3. Modelización Predictiva Multimodelo
Desarrollo y entrenamiento estructurado de cuatro paradigmas clásicos de aprendizaje automático sobre flujos de validación cruzada parametrizada (`cv=5`):
*   **Modelos Lineales:** Regresión Logística de Clasificación.
*   **Modelos de Instancia:** Clasificador por Vecinos más Cercanos (k-NN).
*   **Modelos de Partición Recursiva:** Árbol de Decisión simple y optimizado con control de sobreajuste (*Pruning*).
*   **Ensamble de Modelos:** Bosque Aleatorio (*Random Forest Classifier*).

### 4. Hiper-optimización y Automatización (Pipelines robustos)
*   Encapsulamiento del flujo con la arquitectura `sklearn.pipeline.Pipeline` combinando imputadores dinámicos, escaladores y estimadores finales para prevenir la fuga de información (*Data Leakage*).
*   Uso de **GridSearchCV** para encontrar la configuración algorítmica óptima bajo costo computacional paralelo.

---

## 📊 Resultados Clave & Diagnóstico del Rendimiento

### 🏆 El Modelo Ganador
Tras realizar la optimización con `GridSearchCV`, el **Random Forest Classifier** (parametrizado con `n_estimators=100` y `max_depth=20`) fue coronado como el mejor predictor.

#### Comparativa de Exactitud (Accuracy CV=5):
1.  **Random Forest:** `72.6%` (CV) ➡️ **`74.0%` en Test** 🎉
2.  **Árbol de Decisión:** `69.8%` 
3.  **k-NN:** `66.4%` 
4.  **Regresión Logística:** `62.1%` 

### 🔍 Diagnóstico de Generalización & Explicabilidad
*   **Control de Overfitting:** Se implementó un estudio avanzado de **Permutation Importance** comparando los conjuntos de Entrenamiento (*Train*) vs Prueba (*Test*). Esto demostró que las variables *Sales* (Ventas) y *Profit* (Ganancia) dominan la heurística predictiva, garantizando la estabilidad operativa del pipeline sin depender de ruido circunstancial.

---

## 🛠️ Tecnologías y Librerías Utilizadas
*   **Análisis & Manipulación:** `pandas`, `numpy`
*   **Visualización Científica:** `matplotlib`, `seaborn`
*   **Machine Learning Pipeline:** `scikit-learn`
*   **Ingesta:** `kagglehub`
