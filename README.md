# Heart Disease Prediction (ML)

**Language:** [English](#english) | [Русский](README.ru.md)

---

## English

### Project description

Machine learning project for **binary classification**: predict heart disease (`Absence` / `Presence`) from clinical features (age, blood pressure, cholesterol, ECG-related measures, etc.).

Dataset: classic tabular heart-disease style data (**270 patients**, 13 features + target).

### Key results (test set)

| Metric | Value |
|--------|-------|
| **ROC-AUC** | **~0.91** |
| **Model** | Logistic Regression (`class_weight='balanced'`) |
| **Decision threshold** | tuned with **MIN_PRECISION = 0.65** (higher Presence recall, fewer missed patients) |
| Presence recall (approx.) | **~0.96** |
| Train–Test AUC gap | small (low overfitting) |

### Pipeline highlights

1. EDA (missing values, zeros, class balance)
2. Clinical plausibility checks (ranges based on AHA/ACC, NHLBI ATP III, ADA context, ACC/AHA exercise testing / UCI coding)
3. Train/test split **before** imputation/scaling (no leakage)
4. Median imputation fit on train only + `StandardScaler` for linear/SVM/KNN-family models
5. Model comparison with stratified CV (LogReg, KNN, SVM, Random Forest, Gradient Boosting)
6. GridSearch on the screening-oriented model
7. Threshold tuning for medical screening (`MIN_PRECISION=0.65`)

### How to run

```bash
pip install -r requirements.txt
jupyter notebook heart-disease-prediction.ipynb
```


### Project structure

```
heart-disease-prediction/
├── heart-disease-prediction.ipynb
├── Heart_Disease_Prediction.csv
├── README.md
├── README.ru.md
├── requirements.txt
├── LICENSE
└── .gitignore
```

### Limitations

- Small sample size (n=270) — metrics can vary with split.
- Threshold choice trades precision for recall (more false alarms possible).

### Author

[AnnaKazarian13](https://github.com/AnnaKazarian13)
