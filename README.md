<h1 align="center">Análisis de Inventario y Riesgo de Stockout · Superstore</h1>

<p align="center">
  <a href="https://colab.research.google.com/github/jvillagra66-oss/ml-inventario-superstore/blob/main/notebooks/01_analisis_inventario.ipynb">
    <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Abrir en Colab">
  </a>
  <img src="https://img.shields.io/badge/Python-3.10%2B-3776AB?logo=python&logoColor=white" alt="Python 3.10+">
  <img src="https://img.shields.io/badge/scikit--learn-1.x-F7931E?logo=scikitlearn&logoColor=white" alt="scikit-learn">
  <img src="https://img.shields.io/badge/pandas-2.x-150458?logo=pandas&logoColor=white" alt="pandas">
  <img src="https://img.shields.io/badge/estado-en%20desarrollo-yellow" alt="Estado">
</p>

<p align="center">
  Proyecto de ciencia de datos de punta a punta sobre transacciones de una tienda minorista:
  exploración, limpieza, preprocesamiento, modelos supervisados y segmentación no supervisada
  aplicada a decisiones de inventario.
</p>

---

## Tabla de contenidos

1. [Descripción](#descripción)
2. [Hallazgos principales](#hallazgos-principales)
3. [Dataset](#dataset)
4. [Estructura del repositorio](#estructura-del-repositorio)
5. [Requisitos](#requisitos)
6. [Cómo ejecutar](#cómo-ejecutar)
7. [Recorrido del notebook](#recorrido-del-notebook)
8. [Resultados](#resultados)
9. [Metodología y decisiones de diseño](#metodología-y-decisiones-de-diseño)
10. [Limitaciones y trabajo futuro](#limitaciones-y-trabajo-futuro)
11. [Stack tecnológico](#stack-tecnológico)
12. [Autor](#autor)

---

## Descripción

Este repositorio contiene un notebook que recorre el ciclo completo de un proyecto de ciencia de datos
sobre el dataset **Sample Superstore**: desde la carga y el análisis exploratorio hasta el modelado
supervisado (clasificación y regresión) y el aprendizaje no supervisado (clustering con K-Means),
cerrando con una lectura de negocio de los segmentos encontrados.

El hilo conductor es una pregunta concreta de inventario: **¿qué transacciones tienen riesgo de
quiebre de stock?** Para responderla se construye una variable objetivo binaria a partir del volumen
de unidades vendidas (`Quantity > 3`) y se comparan distintos algoritmos, prestando especial atención
a la capacidad de generalización (train vs. test) y no solo al accuracy.

## Hallazgos principales

- **La complejidad no siempre generaliza.** El árbol de decisión sin podar memoriza el set de
  entrenamiento (accuracy **1,00** en train) y cae a **0,70** en test. El árbol podado
  (`max_depth=3`) rinde **0,651 en train y 0,651 en test**: menos expresivo, pero estable.
- **Random Forest ofrece el mejor equilibrio.** Con 100 árboles alcanza **0,66** de accuracy en test
  y un F1 ponderado de **0,66**, sin sobreajuste, sobre un conjunto de 1.996 registros no vistos.
- **La segmentación no supervisada ordena el negocio.** K-Means con **K=5** separa cinco perfiles
  operativos claramente distintos (Silhouette **0,796**), y el cruce ex-post con la tasa de riesgo de
  stockout permite priorizar políticas de reposición por segmento en lugar de aplicar una regla única.
- **El accuracy solo no alcanza.** Con clases de 57 % / 43 %, un modelo que prediga siempre la clase
  mayoritaria ya obtiene ~0,58: por eso se reportan también precisión, recall, F1 y matriz de confusión.

## Dataset

| Atributo | Detalle |
|---|---|
| Fuente | [Sample Superstore](https://www.kaggle.com/datasets/bravehart101/sample-supermarket-dataset) (Kaggle) |
| Descarga | Automática con `kagglehub`, **sin credenciales** |
| Registros | 9.994 filas × 13 columnas |
| Tras deduplicar | **9.977 filas** (17 duplicados exactos eliminados) |
| Partición | 80 % train (7.981) / 20 % test (1.996), estratificada |
| Variable objetivo | `Stockout_Risk = 1` si `Quantity > 3`, si no `0` |

Variables disponibles: `Ship Mode`, `Segment`, `Country`, `City`, `State`, `Postal Code`, `Region`,
`Category`, `Sub-Category`, `Sales`, `Quantity`, `Discount`, `Profit`.

> El dataset no se versiona en el repositorio: se descarga en tiempo de ejecución para mantener el
> repo liviano y garantizar que siempre se use la misma fuente pública.

## Estructura del repositorio

```text
ml-inventario-superstore/
├── notebooks/
│   └── 01_analisis_inventario.ipynb   # Notebook principal
├── requirements.txt                   # Dependencias del proyecto
└── README.md
```

## Requisitos

- Python **3.10** o superior
- Las dependencias de `requirements.txt`:

```text
pandas
numpy
matplotlib
seaborn
scikit-learn
kagglehub
ipywidgets
```

## Cómo ejecutar

### Opción A — Google Colab (recomendado)

1. Clic en el badge **Open in Colab** del encabezado.
2. Menú *Entorno de ejecución* → **Ejecutar todo**.
3. No hace falta configurar credenciales de Kaggle: `kagglehub` descarga el dataset público
   automáticamente (la primera ejecución tarda unos segundos).

### Opción B — Entorno local

```bash
# 1. Clonar el repositorio
git clone https://github.com/jvillagra66-oss/ml-inventario-superstore.git
cd ml-inventario-superstore

# 2. Crear y activar un entorno virtual
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate

# 3. Instalar dependencias
pip install -r requirements.txt

# 4. Abrir el notebook
jupyter notebook notebooks/01_analisis_inventario.ipynb
```

## Recorrido del notebook

| # | Sección | Qué resuelve | Técnicas |
|---|---|---|---|
| 1 | Carga y exploración (EDA) | Dimensiones, tipos, nulos, duplicados y nulos por columna | `pandas`, `info()`, `isna()`, `duplicated()` |
| 2 | Limpieza | Eliminación de 17 duplicados y de columnas redundantes | Filtrado y selección de variables |
| 3 | Análisis visual | Distribución de ventas y matriz de correlación | `matplotlib`, `seaborn` |
| 4 | Preprocesamiento | Codificación de categóricas y escalado de numéricas | One-Hot, `MinMaxScaler`, `StandardScaler` |
| 5 | Partición | División train/test 80-20 estratificada y reproducible | `train_test_split` (`random_state=42`, `stratify`) |
| 6 | Clasificación base | Riesgo de stockout con modelo lineal y KNN | Regresión Logística, KNN, matriz de confusión |
| 7 | Umbral de decisión | Efecto de mover el umbral de 0,50 a 0,25 | Curva de probabilidad, `classification_report` |
| 8 | Regresión | Predicción continua de ventas | Regresión Lineal, MAE, MSE, R² |
| 9 | Simulador interactivo | Exploración manual de la frontera de decisión | `ipywidgets` |
| 10 | Árboles de decisión | Árbol podado vs. árbol completo (overfitting) | `DecisionTreeClassifier`, `max_depth` |
| 11 | Árbol multiclase | Clasificación en 3 categorías y matriz 3×3 | `DecisionTreeClassifier`, matriz etiquetada |
| 12 | Random Forest | Bosque aleatorio y estabilidad según `n_estimators` | `RandomForestClassifier`, curva de estabilidad |
| 13 | Importancia de variables | Atributos con mayor peso e inferencia | `feature_importances_` |
| 14 | Clustering | Segmentación con K-Means, método del codo y Silhouette | `KMeans`, inercia, `silhouette_score` |
| 15 | Perfiles de clústeres | Caracterización por ventas, ganancias y volumen | Agrupación y promedios |
| 16 | Evaluación ex-post | Tasa de riesgo de stockout por clúster | Cruce supervisado / no supervisado |

## Resultados

Evaluación sobre el conjunto de test (1.996 registros no vistos durante el entrenamiento).

| Modelo | Tarea | Métrica principal | Resultado |
|---|---|---|---|
| Regresión Logística (umbral 0,50) | Clasificación | Accuracy | **0,61** (F1 clase 1 = 0,18) |
| Regresión Logística (umbral 0,25) | Clasificación | Accuracy | **0,62** (F1 clase 1 = 0,25) |
| KNN | Clasificación | Accuracy | **0,66** |
| Árbol podado (`max_depth=3`) | Clasificación | Accuracy train / test | **0,651 / 0,651** |
| Árbol completo (sin podar) | Clasificación | Accuracy train / test | **1,00 / 0,70** → overfitting |
| Árbol multiclase (3 clases) | Clasificación | Accuracy | **0,65** |
| Random Forest (100 árboles) | Clasificación | Accuracy / F1 ponderado | **0,66 / 0,66** |
| Regresión Lineal | Regresión (`Sales`) | MAE · R² | **0,00 · 1,00** ⚠️ (ver limitaciones) |
| K-Means `K=2` | Clustering | Silhouette · Inercia | **0,958 · 12.803,3** |
| K-Means `K=5` (final) | Clustering | Silhouette · Inercia | **0,796 · 5.518,3** |

**Lectura:** el salto de calidad no viene de un modelo más complejo, sino de controlar la
generalización. El árbol podado y el bosque aleatorio empatan en desempeño, pero el bosque lo hace
con menor varianza; el árbol completo ilustra el caso opuesto. En clustering, `K=2` maximiza la
métrica pero `K=5` es la segmentación accionable: los cinco perfiles se traducen en políticas de
inventario distintas.

## Metodología y decisiones de diseño

- **Semilla fija (`random_state=42`)** en todas las particiones y modelos: los resultados son
  reproducibles de principio a fin.
- **Partición estratificada** para conservar la proporción de clases entre train y test.
- **Escalado ajustado solo con train** en los bloques supervisados, para no filtrar información del
  test al entrenamiento.
- **Trazabilidad de la métrica**: cada bloque imprime `classification_report`, matriz de confusión y
  comparación train/test, de modo que el sobreajuste se detecta a la vista.
- **Del clustering al negocio**: los clústeres no se interpretan por sí solos; se cruzan con la tasa
  de riesgo de stockout para convertirlos en una recomendación operativa.

## Limitaciones y trabajo futuro

- [ ] **Fuga de información en el bloque de regresión**: reporta `R² = 1,00` y `MAE = 0,00`, un
      resultado imposible en producción. Hay que revisar que la variable objetivo no esté entre las
      predictoras y volver a evaluar.
- [ ] **Métricas por clase**: el accuracy oculta el desempeño sobre la clase minoritaria. Conviene
      reportar F1 de la clase 1, ROC-AUC y matriz de confusión en todos los modelos.
- [ ] **Búsqueda de hiperparámetros**: incorporar `GridSearchCV` / `RandomizedSearchCV` con
      validación cruzada en lugar de valores fijos.
- [ ] **Persistencia del modelo**: exportar el pipeline final (`joblib`) para poder servirlo desde
      una API.
- [ ] **Automatización**: agregar un `.gitignore` y un workflow de CI que ejecute el notebook de
      punta a punta en cada push.
- [ ] **Datos versionados**: evaluar DVC o un fixture reducido para pruebas sin depender de la
      descarga externa.

## Stack tecnológico

| Área | Herramientas |
|---|---|
| Datos | `pandas`, `numpy`, `kagglehub` |
| Visualización | `matplotlib`, `seaborn` |
| Machine Learning | `scikit-learn` (clasificación, regresión, clustering, métricas) |
| Interacción | `ipywidgets` |
| Entorno | Jupyter Notebook / Google Colab |

## Autor

**jvillagra66-oss** · [GitHub](https://github.com/jvillagra66-oss)

Proyecto con fines educativos y de portafolio. No hay licencia declarada: consultar con el autor antes
de reutilizar el código o los resultados.
