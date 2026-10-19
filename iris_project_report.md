
# Iris Flower Species Classification
## End-to-End Data Science Project Report

**Author:** [Aditya Kumar Rai]  
**Date:** May 2026  
**Tools:** Python, Pandas, Seaborn, Matplotlib, Scikit-learn  

---

## 1. Executive Summary
This project developed a machine learning model to automatically classify Iris 
flowers into three species — Setosa, Versicolor, and Virginica — using four 
physical measurements: sepal length, sepal width, petal length, and petal width. 
A Decision Tree Classifier was trained on 120 samples and evaluated on 30 unseen 
samples, achieving a final accuracy of 96.7%. The model correctly identified 29 
out of 30 flowers in the test set.

---

## 2. Business Problem
A botanist in the field needs to classify an Iris flower into one of three species 
using only four physical measurements taken with a ruler. Manual classification 
requires expertise and reference materials that may not always be available. An 
automated classification model would save time, reduce human error, and provide 
instant identification in field conditions.

**Problem type:** Supervised multi-class classification  
**Success metric:** Accuracy on unseen test data  
**Target variable:** Species (Setosa, Versicolor, Virginica)  

---

## 3. Dataset Description
- **Source:** Seaborn built-in dataset (originally UCI Machine Learning Repository)
- **Size:** 150 rows × 5 columns
- **Class balance:** Perfectly balanced — 50 flowers per species
- **Missing values:** None
- **Features:** sepal_length, sepal_width, petal_length, petal_width (all in cm)

---

## 4. Exploratory Data Analysis (EDA)

### 4.1 Key Findings
The EDA revealed that petal measurements are the most discriminating features 
for species classification:

- **Setosa** is completely separable from the other two species using petal 
  dimensions alone. Its petal length (mean: 1.46cm) is dramatically smaller 
  than Versicolor (mean: 4.26cm) and Virginica (mean: 5.55cm).
- **Versicolor and Virginica** show partial overlap in petal dimensions, 
  making them the harder pair to distinguish — this was later confirmed by 
  the model's single misclassification.
- **Sepal width** showed the weakest discriminating power, with heavily 
  overlapping distributions across all three species.

### 4.2 Correlation Analysis
The heatmap revealed a very high correlation (r = 0.96) between petal_length 
and petal_width, indicating near-redundancy. Despite this, both features were 
retained as the Decision Tree algorithm handles correlated features natively 
by selecting the most informative split at each node.

---

## 5. Data Preparation

### 5.1 Feature Engineering
No new features were engineered. All four original measurements were retained 
as features based on EDA findings.

### 5.2 Label Encoding
The target variable (species) was encoded from string labels to integers:
- Setosa → 0
- Versicolor → 1  
- Virginica → 2

### 5.3 Train/Test Split
The dataset was split into 80% training (120 samples) and 20% test (30 samples) 
using stratified sampling to preserve class proportions in both sets.

---

## 6. Modeling

### 6.1 Algorithm Selection
A **Decision Tree Classifier** was selected for the following reasons:
- Interpretable: the decision rules can be visualized and explained
- Handles both numerical features and multi-class targets natively
- No feature scaling required
- Suitable for small datasets

### 6.2 Hyperparameters
- **max_depth = 3:** Limits tree depth to prevent overfitting
- **random_state = 42:** Ensures reproducibility

### 6.3 How the Model Works
The tree learned to classify flowers using a series of binary questions:
1. Is petal_length ≤ 2.45cm? → If YES: Setosa (immediate answer)
2. If NO: Is petal_width ≤ 1.75cm? → If YES: Versicolor, If NO: Virginica

This mirrors the visual patterns observed during EDA, confirming that the 
model learned genuine biological patterns rather than noise.

---

## 7. Evaluation Results

### 7.1 Overall Accuracy
**96.7%** (29/30 correct predictions on unseen test data)

### 7.2 Confusion Matrix Analysis
| Species | Correct | Misclassified | Notes |
|---|---|---|---|
| Setosa | 10/10 | 0 | Perfect — fully separable |
| Versicolor | 9/10 | 1 (as Virginica) | Expected overlap from EDA |
| Virginica | 10/10 | 0 | Perfect |

### 7.3 Classification Report Summary
| Species | Precision | Recall | F1-Score |
|---|---|---|---|
| Setosa | 1.00 | 1.00 | 1.00 |
| Versicolor | 1.00 | 0.90 | 0.95 |
| Virginica | 0.91 | 1.00 | 0.95 |
| **Overall** | **0.97** | **0.97** | **0.97** |

### 7.4 Feature Importance
Petal dimensions dominated the model's decisions, consistent with EDA findings. 
Sepal width contributed negligibly — confirming the visual patterns observed 
in the box plots and scatter plots.

---

## 8. Conclusions

1. **The model achieved 96.7% accuracy**, correctly classifying 29 of 30 
   unseen flowers — a strong result for a first machine learning model.
2. **Petal measurements are the key discriminators** for Iris species 
   classification, as identified during EDA and confirmed by feature importance.
3. **The single misclassification** (1 Versicolor predicted as Virginica) 
   was anticipated from EDA analysis, where partial overlap between these 
   two species was clearly visible in the pairplot.
4. **The Decision Tree is interpretable** — its decision rules can be 
   explained to a non-technical botanist in plain language.

---

## 9. Limitations & Future Work
- The dataset is small (150 samples) and may not represent all real-world 
  Iris variation. A larger dataset would improve robustness.
- Other algorithms (Random Forest, SVM, KNN) could be tested and compared.
- Cross-validation (k-fold) would give a more reliable accuracy estimate 
  than a single train/test split.
- Deployment as a simple web app (using Flask or Streamlit) would allow 
  botanists to input measurements and get instant predictions.

---

## 10. References
- Fisher, R.A. (1936). The use of multiple measurements in taxonomic problems.
- Scikit-learn Documentation: https://scikit-learn.org
- Seaborn Documentation: https://seaborn.pydata.org