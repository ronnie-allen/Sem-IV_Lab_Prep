# Exercise 7: Support Vector Machine (SVM) for Classification and Regression using Python

## 🔹 **1. Classification: Effect of Kernel Types (Iris Dataset)**

```python
from sklearn import datasets
from sklearn.model_selection import train_test_split
from sklearn.svm import SVC
from sklearn.metrics import accuracy_score

# Load dataset
iris = datasets.load_iris()
X, y = iris.data, iris.target

# Train-test split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3)

# Try different kernels
kernels = ['linear', 'poly', 'rbf', 'sigmoid']
for kernel in kernels:
    model = SVC(kernel=kernel)
    model.fit(X_train, y_train)
    preds = model.predict(X_test)
    acc = accuracy_score(y_test, preds)
    print(f"{kernel.capitalize()} Kernel Accuracy: {acc:.4f}")
```

### ✅ Explanation:
- `kernel`: Determines the transformation applied to data before classification.
- `linear`: Straight-line decision boundary
- `poly`: Polynomial features
- `rbf`: Gaussian function for non-linear patterns
- `sigmoid`: S-shaped curve (like neural networks)

---

## 🔧 **2. Hyperparameter Tuning with GridSearchCV (Breast Cancer Dataset)**

```python
from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import GridSearchCV

# Load dataset
data = load_breast_cancer()
X, y = data.data, data.target

# Parameter grid
param_grid = {
    'C': [0.1, 1, 10],
    'gamma': [0.01, 0.1, 1],
    'kernel': ['rbf', 'linear']
}

grid = GridSearchCV(SVC(), param_grid, refit=True, cv=5)
grid.fit(X, y)

print("Best Parameters:", grid.best_params_)
print("Best Accuracy:", grid.best_score_)
```

### ✅ Explanation:
- `C`: Penalty for misclassification. High C = lower bias, but may overfit.
- `gamma`: Influences decision boundary. High gamma = tight boundaries (may overfit).
- `GridSearchCV`: Exhaustive search over parameter grid using cross-validation.

---

## 🔢 **3. Multiclass Classification (MNIST Digits Dataset)**

```python
from sklearn.datasets import load_digits
from sklearn.svm import SVC
from sklearn.metrics import classification_report

# Load MNIST-like dataset
digits = load_digits()
X, y = digits.data, digits.target

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

model = SVC(kernel='rbf', gamma=0.001, C=10)
model.fit(X_train, y_train)
preds = model.predict(X_test)

print(classification_report(y_test, preds))
```

### ✅ Explanation:
- `SVC` handles multiclass automatically using one-vs-one strategy.
- `classification_report`: Precision, recall, F1-score for each digit class.

---

## 🚗 **4. Regression with SVR + Hyperparameter Tuning (Car Price Prediction)**

```python
import pandas as pd
from sklearn.svm import SVR
from sklearn.model_selection import train_test_split, GridSearchCV
from sklearn.preprocessing import StandardScaler

# Sample custom dataset
data = pd.DataFrame({
    'mileage': [10000, 20000, 15000, 12000, 25000],
    'engine_size': [1.2, 1.6, 1.5, 1.4, 2.0],
    'age': [3, 4, 2, 3, 5],
    'price': [500000, 450000, 480000, 510000, 400000]
})

X = data[['mileage', 'engine_size', 'age']]
y = data['price']

# Scale features
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

# Split
X_train, X_test, y_train, y_test = train_test_split(X_scaled, y, test_size=0.2)

# Grid search
param_grid = {
    'C': [0.1, 1, 10],
    'epsilon': [0.1, 0.2, 0.5],
    'kernel': ['rbf']
}

svr = SVR()
grid = GridSearchCV(svr, param_grid, cv=3)
grid.fit(X_train, y_train)

print("Best SVR Params:", grid.best_params_)
print("SVR R² Score:", grid.score(X_test, y_test))
```

### ✅ Explanation:
- `SVR`: Support Vector Regression
- `epsilon`: Insensitive region where errors don’t get penalized
- `C`: Regularization (like classification)
- `StandardScaler`: SVR requires scaled features

---

## 🎓 SVM Recap Table

| **Concept**            | **Tool/Function**         | **Details**                                      |
|------------------------|---------------------------|--------------------------------------------------|
| Classification Kernels | `SVC(kernel='rbf')`       | Choose from linear, poly, rbf, sigmoid           |
| Regression             | `SVR()`                   | Predict continuous values                        |
| Hyperparameter Tuning  | `GridSearchCV()`          | Grid search over parameters (C, gamma, kernel)   |
| Multiclass             | `SVC()` (auto handles)    | One-vs-One internally                            |
| Accuracy Metric        | `accuracy_score()`        | For classification tasks                         |
| Regression Score       | `model.score()` (R²)      | Coefficient of determination for regression      |

---
Made with 🫶🏻 by Ronnie Allen