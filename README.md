<div align="center">

# 🩺 Diabetes Prediction System

### Machine Learning–Based Diabetes Risk Classification with LightGBM

[![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=flat-square&logo=python&logoColor=white)](https://www.python.org/)
[![LightGBM](https://img.shields.io/badge/LightGBM-Gradient%20Boosting-9ACD32?style=flat-square)](https://lightgbm.readthedocs.io/)
[![Scikit-learn](https://img.shields.io/badge/Scikit--learn-ML%20Evaluation-F7931E?style=flat-square&logo=scikit-learn&logoColor=white)](https://scikit-learn.org/)
[![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?style=flat-square&logo=pandas&logoColor=white)](https://pandas.pydata.org/)

Diabetes prediction using AI/ML analyzes patient data patterns — like glucose levels and BMI — to classify and predict diabetes risk effectively.

**Model accuracy: 87.89%** on the held-out test set.

</div>

---

## 📖 Table of Contents

- [Project Description](#-project-description)
- [Dataset](#-dataset)
- [Key Features](#-key-features)
- [Notebook Workflow](#-notebook-workflow)
- [Sample Visualizations](#-sample-visualizations)
- [Model Results](#-model-results)
- [Technology Stack](#️-technology-stack)
- [Installation & Usage](#-installation--usage)
- [Required Packages](#-required-packages)
- [Acknowledgments](#-acknowledgments)

---

## 📌 Project Description

The **Diabetes Prediction System** is a machine learning project that predicts the likelihood of diabetes in individuals based on health metrics such as age, BMI, HbA1c level, blood glucose level, hypertension, heart disease, gender, and smoking history. It uses a **LightGBM classifier** and covers the full pipeline: data cleaning, exploratory data analysis (EDA), feature engineering, class balancing, outlier removal, model training, and evaluation — all implemented in a single Jupyter notebook (`Diabetes_Prediction.ipynb`).

---

## 📊 Dataset

The notebook loads `diabetes_prediction_dataset.csv`, containing **100,000 rows and 9 columns**:

| Column | Description |
|---|---|
| `gender` | Female / Male / Other |
| `age` | Patient age |
| `hypertension` | 0 = No, 1 = Yes |
| `heart_disease` | 0 = No, 1 = Yes |
| `smoking_history` | never / former / current / No Info / ever / not current |
| `bmi` | Body Mass Index |
| `HbA1c_level` | Hemoglobin A1c level |
| `blood_glucose_level` | Blood glucose level |
| `diabetes` | Target — 0 = No diabetes, 1 = Diabetes |

Initial class distribution: **91,500 non-diabetic vs. 8,500 diabetic** cases — highly imbalanced, which is addressed later in the pipeline (see [Notebook Workflow](#-notebook-workflow)).

---

## ✨ Key Features

| Feature | Description |
|---|---|
| 🧹 **Data Cleaning** | Standardizes `smoking_history` categories (`ever`→`never`, `not current`→`former`), drops `No Info` and `Other` gender rows |
| 📊 **Exploratory Data Analysis (EDA)** | Correlation heatmap, gender/smoking-history vs. diabetes distributions, age distribution |
| ⚖️ **Class Balancing** | Random undersampling of the majority class to fix the 91,500 : 8,500 imbalance |
| 📉 **Outlier Removal** | IQR-based outlier removal on `bmi` and `HbA1c_level` |
| ⚙️ **Feature Engineering** | One-hot encoding of `smoking_history`, label encoding of `gender`, standardization via `StandardScaler` |
| 🧠 **Model Training** | `LGBMClassifier` from LightGBM |
| ✅ **Model Evaluation** | Accuracy, classification report, and confusion matrix |

---

## 🔄 Notebook Workflow

1. **Install & import libraries** — `lightgbm`, `pandas`, `numpy`, `seaborn`, `matplotlib`, `scikit-learn`
2. **Load and explore the dataset** — shape, class balance, dtypes, missing values
3. **Data cleaning**
   - Standardize `smoking_history`, drop `No Info` rows → **64,172 rows** remain
   - Drop `Other` gender rows, encode `Female`→0, `Male`→1
   - One-hot encode `smoking_history` into `smoking_history_current`, `smoking_history_former`, `smoking_history_never`
4. **Exploratory Data Analysis** — correlation heatmap; gender, smoking history, and age distributions
5. **Handle class imbalance** — undersample the majority class to **7,046 vs. 7,046** (perfectly balanced)
6. **Handle outliers** — IQR-based removal on `bmi` and `HbA1c_level`
7. **Train/test split** — 75% / 25% split (`train_test_split`, `random_state=42`)
8. **Feature scaling** — `StandardScaler` fit on training data, applied to both sets
9. **Model training** — `LGBMClassifier()` fit on the scaled, balanced training data
10. **Model evaluation** — accuracy score, classification report, confusion matrix

---

## 🖼️ Sample Visualizations

<div align="center">
<img src="images/correlation_heatmap.png" alt="Correlation Heatmap" width="700"/>
</div>

<div align="center">
<img src="images/eda_gender_smoking_age.png" alt="Gender vs Diabetes, Smoking History vs Diabetes, Age Distribution" width="450"/>
</div>

<div align="center">
<img src="images/bmi_boxplot.png" alt="BMI After Outlier Removal" width="480"/>
<img src="images/hba1c_boxplot.png" alt="HbA1c Level After Outlier Removal" width="480"/>
</div>

These are the actual output images from the notebook run.

---

## 📈 Model Results

After balancing (7,046 / 7,046) and an outlier-cleaned, scaled training set of **8,348 samples**, the LightGBM model achieves:

```
Accuracy: 87.89%

Classification Report:
              precision    recall  f1-score   support

           0       0.91      0.88      0.89      1574
           1       0.85      0.88      0.86      1209

    accuracy                           0.88      2783
   macro avg       0.88      0.88      0.88      2783
weighted avg       0.88      0.88      0.88      2783
```

<div align="center">
<img src="images/confusion_matrix.png" alt="Confusion Matrix" width="480"/>
</div>

---

## 🛠️ Technology Stack

<div align="center">

| Category | Tools |
|---|---|
| **Language** | Python 3.x |
| **Data Handling** | Pandas, NumPy |
| **Machine Learning** | LightGBM (`LGBMClassifier`), Scikit-learn |
| **Visualization** | Matplotlib, Seaborn |
| **Environment** | Jupyter Notebook |

</div>

---

## 📦 Installation & Usage

**1. Install dependencies**
```bash
pip install lightgbm
pip install pandas numpy matplotlib seaborn scikit-learn
```

**2. Add the dataset**
Place `diabetes_prediction_dataset.csv` in the project directory.

**3. Run the notebook**
```bash
jupyter notebook Diabetes_Prediction.ipynb
```
Run all cells top to bottom — the notebook performs cleaning, EDA, balancing, outlier removal, training, and evaluation in sequence.

---

## 📋 Required Packages

```
lightgbm
pandas
numpy
seaborn
matplotlib
scikit-learn
```

---

## 🙏 Acknowledgments

- [**LightGBM**](https://lightgbm.readthedocs.io/) — efficient gradient boosting classifier used for prediction
- [**Scikit-learn**](https://scikit-learn.org/) — train/test split, `StandardScaler`, evaluation metrics
- [**Seaborn**](https://seaborn.pydata.org/) & [**Matplotlib**](https://matplotlib.org/) — data visualization

---

## ⭐ Support

If you found this project useful, consider giving it a **⭐ star** on GitHub!

<div align="center">

Made with ❤️ and 🧠 by [Kruthik JP](https://github.com/Kruthik-JP)

</div>
