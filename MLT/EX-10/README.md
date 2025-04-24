# Exercise 10: Gaussian Mixture Models (GMM) for Clustering using Python

## 📌 **What is a Gaussian Mixture Model (GMM)?**

A **Gaussian Mixture Model** is a probabilistic model that assumes all the data points are generated from a mixture of several Gaussian distributions with unknown parameters.

### 📍 Used for:
- **Clustering** (similar to KMeans but more flexible)
- **Density estimation**
- Can model **elliptical clusters**, unlike KMeans (which assumes spherical)

---

## ✅ **Exercise Task**

### 👉 Implement GMM on the **Iris Dataset**
1. Load and preprocess the data
2. Use `GaussianMixture` from `sklearn.mixture`
3. Cluster the dataset into **3 clusters**
4. Visualize the clustering results
5. Evaluate using **Silhouette Score**

---

## 🧪 **Python Implementation**

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.datasets import load_iris
from sklearn.mixture import GaussianMixture
from sklearn.metrics import silhouette_score
from sklearn.decomposition import PCA

# Load Iris dataset
iris = load_iris()
X = iris.data
y = iris.target

# Apply GMM clustering
gmm = GaussianMixture(n_components=3, random_state=42)
labels = gmm.fit_predict(X)

# Evaluate with Silhouette Score
sil_score = silhouette_score(X, labels)
print(f"Silhouette Score: {sil_score:.3f}")

# Use PCA for 2D visualization
pca = PCA(n_components=2)
X_reduced = pca.fit_transform(X)

# Plot the clustered data
plt.figure(figsize=(8, 5))
plt.scatter(X_reduced[:, 0], X_reduced[:, 1], c=labels, cmap='viridis', s=50)
plt.title('GMM Clustering of Iris Dataset (PCA Reduced)')
plt.xlabel('PCA Component 1')
plt.ylabel('PCA Component 2')
plt.grid(True)
plt.show()
```

---

## 📊 **Silhouette Score - Evaluation Metric**

- **Silhouette Score** ranges from -1 to 1:
  - **+1**: well clustered
  - **0**: overlapping clusters
  - **-1**: wrong clustering

---

## 🔍 **GMM vs KMeans – Why Use GMM?**

| Feature              | KMeans             | GMM                              |
|----------------------|--------------------|----------------------------------|
| Cluster Shape        | Spherical          | Elliptical / Flexible            |
| Model Type           | Hard Assignment    | Soft Assignment (probabilistic)  |
| Use of Probabilities | ❌ No              | ✅ Yes                            |
| Density Estimation   | ❌ No              | ✅ Yes                            |

---

### **Cheatsheet for Gaussian Mixture Models (GMM)**

| **Step**                                    | **Code Snippet**                                                                                 | **Explanation**                                                                                                                                              |
|---------------------------------------------|-------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **1. Import Libraries**                    | `from sklearn.mixture import GaussianMixture`<br>`from sklearn.datasets import load_iris`<br>`from sklearn.metrics import silhouette_score` | Import necessary libraries for GMM and evaluation (Silhouette Score).                                                                                       |
| **2. Load Dataset**                        | `iris = load_iris()`<br>`X = iris.data`<br>`y = iris.target`                                        | Load the Iris dataset (or any other dataset) using `load_iris()` and extract features (`X`) and target labels (`y`).                                          |
| **3. Initialize GMM**                      | `gmm = GaussianMixture(n_components=3, random_state=42)`                                         | Initialize the GMM model with the desired number of components (clusters), and a random state for reproducibility.                                            |
| **4. Fit GMM and Predict Clusters**        | `labels = gmm.fit_predict(X)`                                                                    | Fit the GMM to the data and predict the cluster labels for each data point.                                                                                 |
| **5. Evaluate Model with Silhouette Score**| `sil_score = silhouette_score(X, labels)`<br>`print(f"Silhouette Score: {sil_score:.3f}")`        | Evaluate the clustering quality using the Silhouette Score, which measures how similar a point is to its own cluster compared to others.                      |
| **6. Dimensionality Reduction for Plotting**| `from sklearn.decomposition import PCA`<br>`pca = PCA(n_components=2)`<br>`X_reduced = pca.fit_transform(X)` | Apply **PCA (Principal Component Analysis)** to reduce the dimensionality to 2D for visualization.                                                          |
| **7. Visualize Clusters**                  | `plt.scatter(X_reduced[:, 0], X_reduced[:, 1], c=labels, cmap='viridis', s=50)`<br>`plt.show()`    | Plot the 2D clusters using a scatter plot with color-coded clusters (`c=labels`). Use PCA-reduced data for visualization.                                    |
| **8. Interpret Silhouette Score**          | -                                                                                               | Silhouette Score > 0.5 indicates good clustering, 0 means overlapping clusters, and negative values suggest poor clustering.                                |

---

### **Functions and Methods Used in GMM**

| **Function**                               | **Description**                                                                                                                                         |
|--------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| `GaussianMixture(n_components=3)`          | Initialize a GMM model with a specified number of components (clusters).                                                                                |
| `fit(X)`                                   | Fit the GMM to the feature data `X` and estimate the parameters of the Gaussian distributions.                                                        |
| `fit_predict(X)`                           | Fit the GMM and return the cluster labels (assignments) for each data point.                                                                            |
| `silhouette_score(X, labels)`              | Calculate the Silhouette Score to evaluate clustering performance. Higher values indicate better clustering.                                           |
| `PCA(n_components=2)`                      | Initialize PCA to reduce the dataset to 2 components (for visualization).                                                                              |
| `fit_transform(X)`                         | Apply PCA to reduce data dimensions, returning the transformed dataset in reduced dimensionality.                                                      |
| `plt.scatter(X, y, c=labels, cmap='viridis')` | Create a scatter plot where `X` and `y` represent the data points, `c=labels` assigns different colors for each cluster.                                |

---

### **Visualizing the Clusters**

- **Matplotlib** is commonly used for plotting the clustering results.
- **PCA** is useful for reducing the dimensionality of the data to 2D for easy visualization when dealing with multi-dimensional data.

### **Example Code for Plotting (in 2D)**

```python
import matplotlib.pyplot as plt

# Plot the clustering results (using PCA for 2D reduction)
plt.figure(figsize=(8, 5))
plt.scatter(X_reduced[:, 0], X_reduced[:, 1], c=labels, cmap='viridis', s=50)
plt.title('GMM Clustering of Iris Dataset (PCA Reduced)')
plt.xlabel('PCA Component 1')
plt.ylabel('PCA Component 2')
plt.grid(True)
plt.show()
```

---

### **Interpretation of Results**

- **Silhouette Score** is an indicator of how well each data point has been clustered:
  - **Closer to 1**: Good clustering (distinct clusters).
  - **Around 0**: Overlapping clusters.
  - **Negative**: Poor clustering.

---

This cheatsheet summarizes the key functions and steps required to implement **Gaussian Mixture Models (GMM)** in Python for clustering tasks, along with code snippets, explanations, and how to evaluate the results effectively.

Let me know if you need additional details or specific explanations on any part!

## 🧠 **Conclusion**

- GMM is more powerful than KMeans when clusters are not perfectly spherical.
- Soft clustering lets each point belong to multiple clusters with different probabilities.
- PCA helps in visualization if features are > 2.
- Silhouette score helps objectively evaluate clustering quality.

---
Made with by Ronnie Allen
