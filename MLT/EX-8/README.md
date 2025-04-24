# Exercise 8 —Implementing AdaBoost Algorithm and Boosting Ensemble Technique using Python

## 🔍 **🔹 What is AdaBoost? (Adaptive Boosting)**

**AdaBoost** is an ensemble learning technique that combines multiple **weak learners** (usually decision stumps) to create a **strong classifier**.  
It works by sequentially training classifiers, with each one **focusing more on the errors** of the previous one.

- Boosting = Train models **sequentially**
- Each model fixes the errors of the previous one
- In AdaBoost, **samples misclassified** get **higher weights** in the next model

---

## 🧪 **Exercise Questions Breakdown**

### ✅ **1. Compare SVM and AdaBoost on Iris Dataset**

#### 🔧 Code:
```python
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.svm import SVC
from sklearn.ensemble import AdaBoostClassifier
from sklearn.metrics import classification_report

# Load dataset
X, y = load_iris(return_X_y=True)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3)

# SVM Model
svm = SVC(probability=True)
svm.fit(X_train, y_train)
svm_preds = svm.predict(X_test)

# AdaBoost Model
ada = AdaBoostClassifier()
ada.fit(X_train, y_train)
ada_preds = ada.predict(X_test)

# Evaluation
print("SVM Performance:\n", classification_report(y_test, svm_preds))
print("AdaBoost Performance:\n", classification_report(y_test, ada_preds))
```

#### 💡 Explanation:
- `SVC()`: A Support Vector Machine classifier
- `AdaBoostClassifier()`: Combines multiple decision stumps to form a strong classifier
- `classification_report()`: Returns precision, recall, F1-score, and support

---

### ✅ **2. Tune AdaBoost with Decision Tree Base (Stump)**

#### 🔧 Code:
```python
from sklearn.tree import DecisionTreeClassifier
from sklearn.model_selection import GridSearchCV

# Weak learner
base = DecisionTreeClassifier(max_depth=1)

# AdaBoost with hyperparameter grid
params = {
    'n_estimators': [10, 50, 100],
    'learning_rate': [0.01, 0.1, 1.0]
}

ada = AdaBoostClassifier(base_estimator=base)
grid = GridSearchCV(ada, params, cv=5, scoring='accuracy')
grid.fit(X_train, y_train)

# Results
print("Best Parameters:", grid.best_params_)
print("Best Accuracy:", grid.best_score_)
```

#### 💡 Explanation:
- `n_estimators`: Number of boosting rounds
- `learning_rate`: Shrinks contribution of each tree
- `GridSearchCV`: Automates testing combinations of parameters

---

## 🎯 Cheatsheet Table (Code + Explanation)

| **Concept**                       | **Code Snippet**                                     | **Explanation**                                                                 |
|----------------------------------|------------------------------------------------------|---------------------------------------------------------------------------------|
| Load Iris dataset                | `load_iris(return_X_y=True)`                        | Loads features `X` and labels `y`                                               |
| Train/test split                 | `train_test_split(X, y)`                            | Splits the dataset into training and testing                                   |
| Train SVM                        | `SVC().fit(X_train, y_train)`                       | Trains a baseline classifier                                                   |
| Train AdaBoost                   | `AdaBoostClassifier().fit(X_train, y_train)`        | Trains AdaBoost using decision stumps                                          |
| Evaluate model                   | `classification_report(y_test, preds)`             | Outputs precision, recall, and F1-score                                        |
| Use decision stump               | `DecisionTreeClassifier(max_depth=1)`              | Base learner for AdaBoost                                                      |
| Hyperparameter tuning            | `GridSearchCV()`                                    | Searches optimal `n_estimators`, `learning_rate`                               |
| Get best model params            | `grid.best_params_`                                 | Returns best parameters found during tuning                                    |

---

## 🧠 Key Concepts:

| **Term**         | **Explanation**                                                                 |
|------------------|----------------------------------------------------------------------------------|
| Weak Learner     | A model that performs slightly better than random guess (e.g., depth-1 tree)    |
| Boosting         | Technique that trains models sequentially to correct predecessors’ errors       |
| Learning Rate    | Controls the weight of each new model in the ensemble                           |
| n_estimators     | Number of weak learners to combine                                              |
| Decision Stump   | A tree with only one split; used as a weak learner                              |
| GridSearchCV     | Automated way to test different hyperparameter values with cross-validation     |

---

## 📊 Sample Output:
```
SVM Performance:
              precision    recall  f1-score   support
...

AdaBoost Performance:
              precision    recall  f1-score   support
...

Best Parameters: {'learning_rate': 0.1, 'n_estimators': 50}
Best Accuracy: 0.9667
```

---
Made with 🫶🏻 by Ronnie Allen