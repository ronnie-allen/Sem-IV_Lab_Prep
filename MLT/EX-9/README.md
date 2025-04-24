# Exercise 9: Implementing Random Forest Algorithm

## 🌳 What is **Random Forest**?

**Random Forest** is an **ensemble learning method** that builds multiple decision trees and merges them to get a more accurate and stable prediction.

- It uses **Bagging** (Bootstrap Aggregating).
- Combats **overfitting** better than a single decision tree.
- Useful for both **classification** and **regression** problems.

---

## 🔹 Exercise 9: Tasks Overview

### ✅ **1. Random Forest Classification on Iris Dataset**

#### 📌 Steps:
1. Read and preprocess the dataset
2. Choose `X` (features) and `y` (target)
3. Create models with different hyperparameters
4. Calculate predictions and evaluate
5. Display confusion matrix, accuracy, precision, recall, F1-score

---

### 🔧 **Code Implementation:**

```python
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import classification_report, confusion_matrix
import pandas as pd

# Load Iris dataset
iris = load_iris()
X = pd.DataFrame(iris.data, columns=iris.feature_names)
y = pd.Series(iris.target)

# Train/test split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

# Try different parameters
models = [
    RandomForestClassifier(n_estimators=10),
    RandomForestClassifier(n_estimators=50, max_depth=3),
    RandomForestClassifier(n_estimators=100, max_depth=5, min_samples_split=4),
    RandomForestClassifier(n_estimators=150, max_depth=7, min_samples_split=3)
]

# Train & evaluate
for i, model in enumerate(models, 1):
    model.fit(X_train, y_train)
    y_pred = model.predict(X_test)
    print(f"\nModel {i} Evaluation:")
    print(confusion_matrix(y_test, y_pred))
    print(classification_report(y_test, y_pred))
```

---

### ✅ **2. Hyperparameter Tuning Using GridSearchCV**

```python
from sklearn.model_selection import GridSearchCV

param_grid = {
    'n_estimators': [10, 50, 100],
    'max_depth': [3, 5, None],
    'min_samples_split': [2, 4, 6]
}

grid = GridSearchCV(RandomForestClassifier(), param_grid, cv=5, scoring='accuracy')
grid.fit(X_train, y_train)

print("Best Parameters:", grid.best_params_)
print("Best Score:", grid.best_score_)
```

---

### ✅ **3. Random Forest Regression on Boston Housing Dataset**

```python
from sklearn.datasets import fetch_california_housing
from sklearn.ensemble import RandomForestRegressor
from sklearn.metrics import mean_squared_error, r2_score

# Load California Housing Dataset (updated version of Boston)
data = fetch_california_housing()
X_r = pd.DataFrame(data.data, columns=data.feature_names)
y_r = data.target

Xr_train, Xr_test, yr_train, yr_test = train_test_split(X_r, y_r, test_size=0.3, random_state=42)

regressor = RandomForestRegressor(n_estimators=100)
regressor.fit(Xr_train, yr_train)
yr_pred = regressor.predict(Xr_test)

print("MSE:", mean_squared_error(yr_test, yr_pred))
print("R² Score:", r2_score(yr_test, yr_pred))
```

---

## 📚 Concepts and Definitions

| Concept                     | Explanation                                                                 |
|-----------------------------|-----------------------------------------------------------------------------|
| **Random Forest**           | Ensemble of decision trees; uses majority voting (classification) or average (regression) |
| **n_estimators**            | Number of trees in the forest                                              |
| **max_depth**               | Maximum depth of each tree                                                 |
| **min_samples_split**       | Minimum number of samples required to split a node                         |
| **confusion matrix**        | Matrix showing TP, TN, FP, FN                                              |
| **precision**               | True Positives / (True Positives + False Positives)                        |
| **recall**                  | True Positives / (True Positives + False Negatives)                        |
| **F1-score**                | Harmonic mean of precision and recall                                      |
| **MSE**                     | Mean Squared Error (average of squared difference between actual and predicted values) |
| **R² score**                | Proportion of variance in the dependent variable explained by the model    |

---

## 🧠 Summary Table

| Task                       | Dataset             | Output Metrics                         |
|---------------------------|---------------------|----------------------------------------|
| RF Classification          | Iris                | Accuracy, Confusion Matrix, Precision, Recall |
| RF + GridSearch            | Iris                | Best Params: n_estimators, depth, etc. |
| RF Regression              | California Housing  | MSE, R² score                          |

---
Made with by Ronnie Allen