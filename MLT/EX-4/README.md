## EX-4

# CONCEPT AND APPLICATIONS OF PRINCIPAL COMPONENT ANALYSIS (PCA) WITH SCIKIT LEARN

🧠 **What is PCA?**
-------------------

**Principal Component Analysis (PCA)** is a technique that transforms your dataset into a set of **linearly uncorrelated features (principal components)**. It helps in:

-   **Reducing dimensions** while preserving maximum variance

-   **Improving model performance**

-   **Visualizing high-dimensional data**

* * * * *

✅ **Common PCA Workflow with Syntax + Explanations**
----------------------------------------------------

| 🔢 Step | 💡 What It Does | 🧪 Python Code Snippet | 🧾 Explanation |
| --- | --- | --- | --- |
| 1 | Load dataset | `df = pd.read_csv('data.csv')` | Read the CSV file using pandas |
| 2 | Handle missing values | `df.fillna(df.mean(numeric_only=True), inplace=True)` | Replace missing numeric values with column mean |
| 3 | Encode categorical | `df = pd.get_dummies(df, drop_first=True)` | One-hot encode categorical variables |
| 4 | Feature scaling | `scaler = StandardScaler(); scaled_data = scaler.fit_transform(df)` | Standardize features for PCA (mean=0, std=1) |
| 5 | Apply PCA | `pca = PCA(); pca_data = pca.fit_transform(scaled_data)` | Perform PCA |
| 6 | Explained variance | `explained_variance = pca.explained_variance_ratio_` | Shows how much variance is captured by each PC |
| 7 | Scree plot | `plt.plot(np.cumsum(explained_variance))` | Visualize cumulative explained variance |
| 8 | Select n PCs | `pca = PCA(n_components=0.95)` | Retain enough PCs to explain 95% variance |
| 9 | Fit & transform | `reduced_data = pca.fit_transform(scaled_data)` | Get reduced dimensional dataset |
| 10 | PCA components | `components = pd.DataFrame(pca.components_, columns=df.columns)` | See weights (loadings) of original features |
| 11 | Visualize loadings | `sns.heatmap(components, cmap='coolwarm')` | See how features contribute to each PC |
| 12 | Visualization (2D) | `sns.scatterplot(x=pca_data[:,0], y=pca_data[:,1])` | Plot 2D PCA-transformed data |
| 13 | Interactive Viz | Use `plotly.express.scatter` or `altair` | Create interactive PCA plots |

* * * * *

🧪 Full Code With Step-by-Step Explanations
-------------------------------------------

```
# STEP 1: Import Libraries
import pandas as pd
import numpy as np
from sklearn.preprocessing import StandardScaler
from sklearn.decomposition import PCA
import matplotlib.pyplot as plt
import seaborn as sns

# STEP 2: Load the dataset
df = pd.read_csv('customer_data.csv')

# STEP 3: Handle missing values
df.fillna(df.mean(numeric_only=True), inplace=True)

# STEP 4: Convert categorical variables using one-hot encoding
df = pd.get_dummies(df, drop_first=True)

# STEP 5: Feature scaling (standardization)
scaler = StandardScaler()
scaled_data = scaler.fit_transform(df)

# STEP 6: Apply PCA
pca = PCA()
pca_data = pca.fit_transform(scaled_data)

# STEP 7: Explained variance
explained_variance = pca.explained_variance_ratio_
cumulative_variance = np.cumsum(explained_variance)

# STEP 8: Plot cumulative explained variance (Scree Plot)
plt.figure(figsize=(10, 5))
plt.plot(cumulative_variance, marker='o', linestyle='--')
plt.xlabel('Number of Principal Components')
plt.ylabel('Cumulative Explained Variance')
plt.title('Explained Variance by Components')
plt.grid()
plt.axhline(y=0.95, color='r', linestyle='-')
plt.show()

# STEP 9: Fit PCA for 95% variance
pca_95 = PCA(n_components=0.95)
reduced_data = pca_95.fit_transform(scaled_data)

# STEP 10: View principal components (loadings)
loadings = pd.DataFrame(pca_95.components_, columns=df.columns)

# STEP 11: Visualize loadings
plt.figure(figsize=(12,6))
sns.heatmap(loadings, cmap='coolwarm', center=0)
plt.title('Feature Loadings for Principal Components')
plt.show()

# STEP 12: Visualize data in 2D
plt.figure(figsize=(8,6))
plt.scatter(reduced_data[:, 0], reduced_data[:, 1], c='blue', edgecolors='k')
plt.xlabel('PC1')
plt.ylabel('PC2')
plt.title('PCA - First Two Principal Components')
plt.grid(True)
plt.show()

```

* * * * *

📋 Cheatsheet Table (Quick Reference)
-------------------------------------

| Step | Function/Method | Purpose |
| --- | --- | --- |
| `fillna(df.mean())` | Handle missing values |  |
| `pd.get_dummies()` | Encode categorical columns |  |
| `StandardScaler()` | Normalize numerical values |  |
| `PCA()` | Create PCA model |  |
| `.fit_transform(data)` | Fit and apply PCA |  |
| `.explained_variance_ratio_` | Variance captured by each PC |  |
| `np.cumsum()` | Cumulative sum of variance |  |
| `sns.heatmap()` | Visualize how features load on PCs |  |
| `pca.components_` | Get weight (importance) of each feature in each PC |  |

* * * * *

🧠 Notes:
---------

-   **Standardization** is crucial because PCA is affected by scale.

-   Always **visualize explained variance** to decide how many PCs to keep.

-   **Loadings** tell you which features are influencing a component.

-   PCA is **unsupervised**, meaning it doesn't use target labels.

* * * * *
