
# 🔍 Diabetes Prediction with MLflow & Random Forest

Este proyecto utiliza **machine learning clásico** (Random Forest Classifier) para predecir si un paciente presenta o no diabetes, con seguimiento de experimentos mediante **MLflow** y una arquitectura modular basada en la metodología de **Pau Labarta**.

---

## 🎯 Objetivo

Desarrollar un pipeline completo de clasificación binaria utilizando datos médicos, enfocado en predecir la diabetes con un modelo clásico optimizado y seguimiento de métricas.

---

## 📦 Dataset

- **Fuente:** Pima Indians Diabetes Database (Kaggle)
- **Tamaño:** 768 muestras × 9 columnas
- **Variables:** Glucosa, IMC, Edad, Embarazos, Presión, Insulina, Pedigrí, etc.
- **Objetivo (Target):** 1 (diabético), 0 (no diabético)

---

## 🧭 Estructura del Proyecto

```
mlflow-diabetes-prediction/
├── data/
│   ├── raw/                  ← Dataset original
│   ├── features/             ← X_train, y_train, X_test, y_test
├── notebooks/
│   ├── 01_eda.ipynb
│   ├── 02_preprocessing.ipynb
│   ├── 03_training_validation.ipynb
│   ├── 04_evaluation_export.ipynb
├── models/                   ← Registro de modelos (MLflow)
├── README.md
└── requirements.txt
```

---

## 🔁 Flujo del Proyecto (Pau Labarta)

1. **EDA & Preprocesamiento**  
   - Revisión de nulos y valores atípicos  
   - Imputación con mediana  
   - `Capping` de outliers severos  
   - `log-transform` para variables asimétricas  
   - `StandardScaler` aplicado  
   - Selección de características vía `mutual_info_classif`

2. **Entrenamiento y Validación**
   - Evaluación de +20 modelos con `LazyPredict`  
   - Selección de **Random Forest** por su balance entre desempeño y tiempo
   - Aplicación de **SMOTE** para balanceo de clases
   - Ajuste de hiperparámetros (`max_depth`, `n_estimators`, `class_weight`, etc.)
   - Registro en **MLflow** con métricas y artefactos

3. **Evaluación Final**
   - Matriz de confusión, curva ROC, y métricas de desempeño
   - Exportación del modelo

---

## 📊 Métricas Finales (Random Forest optimizado)

| Métrica     | Valor     |
|-------------|-----------|
| Accuracy    | 0.7208    |
| Precision   | 0.6491    |
| Recall      | 0.6852    |
| F1-score    | 0.6504    |
| ROC AUC     | 0.7254    |

✅ **SMOTE** ayudó a mejorar el recall para reducir falsos negativos (diagnósticos omitidos).

---

## 💡 Recomendaciones Futuras

- 🔄 Ajuste adicional con `Optuna` o `GridSearchCV` más extenso.
- ⚖️ Probar `class_weight='balanced_subsample'` o ensembles híbridos.
- 📈 Validación cruzada con `StratifiedKFold`.
- 🧪 Comparativa con modelos como `XGBoost`, `LightGBM`.
- 🚀 Publicar como API con FastAPI o desplegar vía Streamlit.

---

## 🧪 Ejecución

```
# Entrenar desde notebook principal
jupyter notebook notebooks/03_training_validation.ipynb
```

---

## 📝 Créditos

Desarrollado por [@alexormx](https://github.com/alexormx) como parte del portafolio final de **AiLab** – Proyecto de clasificación binaria.