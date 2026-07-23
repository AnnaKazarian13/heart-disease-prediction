# Предсказание болезней сердца (ML)

**Язык:** [English](README.md) | [Русский](#русский)

---

## Русский

### Описание проекта

Проект машинного обучения: **бинарная классификация** — предсказать наличие болезни сердца (`Absence` / `Presence`) по клиническим признакам (возраст, АД, холестерин, показатели ЭКГ/нагрузки и др.).

Данные: табличный датасет (**270 пациентов**, 13 признаков + цель).

### Ключевые результаты (test)

| Метрика | Значение |
|---------|----------|
| **ROC-AUC** | **~0.91** |
| **Модель** | Logistic Regression (`class_weight='balanced'`) |
| **Порог решения** | подобран с **MIN_PRECISION = 0.65** (выше Recall Presence, меньше пропусков больных) |
| Recall Presence (примерно) | **~0.96** |
| Разница Train–Test AUC | небольшая (без сильного переобучения) |

### Пайплайн

1. EDA (пропуски, нули, баланс классов)
2. Клинические допустимые диапазоны (AHA/ACC, NHLBI ATP III, ADA-контекст, ACC/AHA exercise / кодировка UCI)
3. `train_test_split` **до** импутации и scaling (без утечки)
4. Медиана только из train + `StandardScaler` для LR/SVM/KNN
5. Сравнение моделей на stratified CV
6. GridSearch для финальной модели
7. Подбор порога для скрининга (`MIN_PRECISION=0.65`)

### Как запустить

```bash
pip install -r requirements.txt
jupyter notebook heart-disease-prediction.ipynb
```


### Структура

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

### Ограничения

- Маленькая выборка (n=270) — метрики зависят от split.
- Низкий порог увеличивает ложные тревоги ради высокого recall.

### Автор

[AnnaKazarian13](https://github.com/AnnaKazarian13)
