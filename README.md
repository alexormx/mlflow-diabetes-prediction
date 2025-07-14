# 🩺 Predicción de Diabetes con MLflow y Random Forest

Este proyecto implementa un flujo completo de Machine Learning tradicional para predecir la probabilidad de diabetes tipo 2 usando el dataset **Pima Indians Diabetes**. Se siguen buenas prácticas de ingeniería de características, comparación de modelos, selección basada en métricas y registro con MLflow. Además, se estructura como servicio de predicción por lotes siguiendo la arquitectura propuesta por Pau Labarta.

---

## 🎯 Objetivo del Proyecto

Predecir la presencia de diabetes a partir de variables clínicas usando modelos de clasificación tradicionales, optimizando el rendimiento mediante preprocesamiento, selección de características, comparación de modelos y ajuste de hiperparámetros.

---

## 📦 Dataset

El dataset contiene 768 registros con las siguientes variables:

- Glucose, BloodPressure, Insulin, BMI, Age, SkinThickness, etc.
- Variable target: `Outcome` (1 = Diabetes, 0 = No Diabetes)

---

## 📊 Flujo del Proyecto

El proyecto sigue el enfoque de **Batch-Prediction Service** propuesto por Pau Labarta:


- 📘 Feature pipeline
- 📙 Training pipeline
- 📒 Batch inference pipeline

Cada etapa está contenida en un notebook independiente, garantizando modularidad, reproducibilidad y trazabilidad.

---

## 📁 Estructura del proyecto

```bash
mlflow-diabetes-prediction/
│
├── data/                      # Dataset original y features procesados
│   ├── diabetes.csv
│   └── features/
│       ├── X_train.csv
│       ├── X_test.csv
│       ├── y_train.csv
│       └── y_test.csv
├── models/                    # Modelos entrenados (pickle, etc.)
├── notebooks/                 # Jupyter notebooks por etapa
│   ├── 01_eda.ipynb
│   ├── 02_preprocessing.ipynb
│   ├── 03_training_validation.ipynb
│   └── 04_evaluation_export.ipynb
├── requirements.txt
├── README.md
└── .gitignore
```

---

## 📊 Dataset utilizado

- **Fuente**: [Kaggle - Pima Indians Diabetes Database](https://www.kaggle.com/datasets/uciml/pima-indians-diabetes-database)
- **Registros**: 768 mujeres mayores de 21 años
- **Variables**: 8 predictoras + 1 objetivo (`Outcome`: 1 = tiene diabetes, 0 = no)

---

## 🔁 Pipeline del proyecto

### 📘 1. Exploración de Datos (EDA)
- Visualización de distribuciones, outliers y valores faltantes
- Análisis de correlación entre variables
- Identificación de datos fisiológicamente imposibles

### 📘 2. Preprocesamiento
- Imputación conservadora de valores faltantes (mediana)
- Capping de outliers extremos por percentiles
- Transformación logarítmica de variables asimétricas
- Análisis de importancia de características (`mutual_info_classif`)
- División en `train/test` y guardado de features para el pipeline de entrenamiento

### 📙 3. Entrenamiento y Validación
- Comparación de modelos con `LazyPredict`
- Entrenamiento de modelos con mejor desempeño (ej. Random Forest, Logistic Regression)
- Justificación de métricas seleccionadas: se priorizó F1-score debido a la necesidad de balance entre Precision y Recall
- Registro de experimentos con **MLflow**

### 📒 4. Evaluación final y exportación
- Métricas: Accuracy, Precision, Recall, F1, ROC AUC
- Exportación del modelo final y métricas clave

---

## 🔍 Hallazgos clave

- `Glucose`, `BMI`, `Age` y `Pregnancies` son las variables más informativas según `mutual_info_classif`.
- El análisis no evidenció multicolinealidad significativa.
- Random Forest logró el mejor rendimiento general (mayor F1).
- Se evitaron transformaciones innecesarias como escalado, ya que el modelo elegido no lo requería.
- El preprocesamiento fue completamente modularizado y versionado.

---

## ⚠️ Notas sobre escalado

El escalado (`StandardScaler`) **no se aplicó** en esta etapa porque el modelo final seleccionado (Random Forest) **no lo requiere**.  
Además, el análisis de importancia de características con `mutual_info_classif` se realiza **antes del escalado**, ya que esta métrica **es invariante a transformaciones de escala**.

---

## 🧪 Requisitos

```bash
pip install -r requirements.txt
```

---

## 🔁 Reproducibilidad

```bash
git clone https://github.com/alexormx/mlflow-diabetes-prediction.git
cd mlflow-diabetes-prediction
python -m venv .venv
source .venv/bin/activate  # En Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

---

## ✍️ Autor
Alejandro Ortiz Lopez  
[LinkedIn](https://www.linkedin.com/in/alexormx/) | GitHub: `@alexormx`

---

## 📌 Licencia

Este proyecto se publica con fines educativos. Puedes usar y modificar el contenido respetando la fuente original del dataset (Kaggle).
