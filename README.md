# XCardio: Heart Disease Prediction (Cleveland Dataset)

Machine learning models to predict the presence of heart disease from clinical features in the UCI Cleveland Heart Disease dataset. Compares several classifiers, including tree-based and boosting models, with hyperparameter tuning.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Prateek-2023/XCardio/blob/main/Heart_Disease_Cleveland_Extended.ipynb)

## Run it in one click
1. Click the **Open In Colab** badge above
2. Go to **Runtime → Run all**
3. No setup needed. Dependencies install in the first cell and the dataset is downloaded automatically.

## Results
Evaluated on a held-out test set of 20,000 samples (80/20 split of the 100,000 rows).

| Model | Test Accuracy |
|-------|---------------|
| Logistic Regression | 81.71% |
| Random Forest | 88.87% |
| **XGBoost (proposed)** | **98.19%** |

**XGBoost detail** (precision, recall and F1 are all 0.98 for both classes):

|  | Predicted: No Disease | Predicted: Disease |
|---|---|---|
| **Actual: No Disease** | 9,829 | 171 |
| **Actual: Disease** | 191 | 9,809 |

The model makes only 362 errors out of 20,000 predictions, and the errors are spread evenly between false positives (171) and false negatives (191).

> These scores come from an extended, synthetically generated dataset (see the Dataset section) and should not be read as real-world clinical performance.

## Approach
1. **Data**: Extended Cleveland Heart Disease dataset (100,000 rows, 13 clinical features, balanced 50/50 target). See the dataset note below.
2. **Preprocessing**: handling missing values, encoding categorical features, scaling
3. **Models**: Logistic Regression (baseline), Random Forest, and XGBoost (proposed model)
4. **Evaluation**: held-out 20,000-sample test set, accuracy, confusion matrix, precision/recall/F1
5. **Key findings**:
   - XGBoost clearly outperforms the other models, about 9 points above Random Forest and 16 points above Logistic Regression.
   - The large gap between the linear baseline and the tree-based models suggests the relationship between features and the target is non-linear.
   - TODO: add the top features by importance (e.g. from XGBoost feature importance or SHAP).

## Repository structure
```
├── Heart_Disease_Cleveland_Extended.ipynb   # main notebook
├── Cleveland_Extended.csv                    # dataset (10 MB)
├── requirements.txt                          # dependencies
├── .gitignore
└── README.md
```

## Run locally (optional)
```bash
git clone https://github.com/Prateek-2023/XCardio.git
cd XCardio
pip install -r requirements.txt
jupyter notebook Heart_Disease_Cleveland_Extended.ipynb
```

## Tech stack
Python, pandas, NumPy, scikit-learn, XGBoost, Matplotlib, Seaborn

## Dataset
`Cleveland_Extended.csv`: 100,000 rows x 14 columns (13 features + binary `target`; 1 = heart disease). No missing values; classes are perfectly balanced (50,000 each).

**Note:** This is an *extended* version of the original UCI Cleveland dataset ([source](https://archive.ics.uci.edu/dataset/45/heart+disease), 303 patients). Continuous values such as `age` and `chol` are non-integer, which indicates the extra rows are synthetically generated or augmented rather than real patient records. Metrics on this data may therefore be higher than on real clinical data and should not be read as clinical performance.

| Column | Meaning |
|---|---|
| age, sex | age, sex |
| cp | chest pain type |
| trestbps | resting blood pressure |
| chol | serum cholesterol |
| fbs | fasting blood sugar > 120 mg/dl |
| restecg | resting ECG result |
| thalachh | max heart rate achieved |
| exang | exercise-induced angina |
| oldpeak | ST depression induced by exercise |
| slope | slope of peak exercise ST segment |
| ca | number of major vessels (0-4) |
| thal | thalassemia status |
| target | heart disease present (1) or not (0) |

## Disclaimer
Educational project only. Not for medical diagnosis.
