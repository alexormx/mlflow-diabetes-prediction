# 🩺 Diabetes Prediction with MLflow

Este proyecto aplica técnicas de Machine Learning tradicional para predecir si una persona padece diabetes, utilizando el conocido dataset **Pima Indians Diabetes**. El enfoque incluye análisis exploratorio, preprocesamiento, modelado, evaluación y seguimiento de experimentos con MLflow.

---

## 📁 Estructura del proyecto

```bash
mlflow-diabetes-prediction/
│
├── data/                      # Dataset original (CSV)
├── models/                    # Modelos entrenados (opcional)
├── notebooks/                 # Jupyter notebooks por etapa
│   ├── 01_eda.ipynb           # Análisis exploratorio (EDA)
│   ├── 02_preprocessing.ipynb # Limpieza, imputación, outliers
│   └── 03_model_training.ipynb# Entrenamiento y evaluación
│
├── mlruns/                    # Experimentos registrados por MLflow
├── requirements.txt           # Librerías necesarias
├── README.md                  # Este archivo
└── .gitignore                 # Archivos ignorados por git

---

## 📊 Dataset utilizado

- **Fuente**: [Kaggle - Pima Indians Diabetes Database](https://www.kaggle.com/datasets/uciml/pima-indians-diabetes-database)
- **Registros**: 768 mujeres mayores de 21 años
- **Variables**: 8 predictoras + 1 objetivo (`Outcome`: 1 = tiene diabetes, 0 = no)

---

## 🚀 Pipeline del proyecto

### 1. Exploración de Datos (EDA) – `01_eda.ipynb`

- Visualización y estadísticos generales del dataset.
- Análisis de la distribución por clase (`Outcome`).
- Identificación de valores erróneos como ceros fisiológicamente imposibles.
- Análisis de correlación entre variables.

### 2. Preprocesamiento – `02_preprocessing.ipynb`

- Imputación de valores faltantes (ceros inválidos → NaN).
- Tratamiento de outliers.
- Escalado de variables numéricas.
- Separación en sets de entrenamiento y prueba.

### 3. Entrenamiento de modelos – `03_model_training.ipynb`

- Modelos evaluados:
  - Logistic Regression
  - Random Forest
  - Support Vector Machine (SVM)
- Métricas comparadas: Accuracy, Precision, Recall, F1, ROC AUC
- Uso de MLflow para rastrear experimentos y parámetros

---

## 🔍 Hallazgos clave

- `Glucose`, `BMI`, `Age` y `Pregnancies` son las variables más correlacionadas con la diabetes.
- No se detectó multicolinealidad severa entre variables predictoras.
- Se realizó imputación conservadora de valores faltantes (como ceros en presión sanguínea, insulina, etc.).
- Random Forest obtuvo la mejor métrica F1 en los experimentos realizados.

---

## 🧪 Requisitos

Instala las dependencias usando:

```bash
pip install -r requirements.txt

## 🔁 Reproducibilidad

### 1. Clona el repositorio:

```bash
git clone https://github.com/alexormx/mlflow-diabetes-prediction.git
cd mlflow-diabetes-prediction

### 2. Crea y activa un entorno virtual:

```bash
python3 -m venv .venv
source .venv/bin/activate

---

### 3. Instala las dependencias:

```bash
pip install -r requirements.txt

---

### 4. Ejecuta los notebooks en orden desde Jupyter:
- 01_eda.ipynb
- 02_preprocessing.ipynb
- 03_model_training.ipynb

---

## ✍️ Autor
Alejandro Ortiz Lopez
LinkedIn | GitHub

---

##  📌 Licencia
Este proyecto se publica con fines educativos. Puedes usar y modificar el contenido respetando la fuente original del dataset (Kaggle).

---