# Ex-1 DATA PREPROCESSING

✅ **1\. Calculate the % of missing values in a column**
-------------------------------------------------------

**Concept**: Missing values (nulls/NaNs) can cause problems in analysis. So, we first identify how many values are missing in each column.

```
missing_percentage = df.isnull().mean() * 100

```

-   `df.isnull()` returns a DataFrame of booleans (True where data is missing).

-   `.mean()` calculates the average of True (1) values column-wise.

-   Multiplying by 100 gives the percentage.

* * * * *

✅ **2\. Replace missing value with mean if % missing < 10%**
------------------------------------------------------------

**Concept**: If a numerical column has very few missing values (less than 10%), we can safely replace those with the **mean**.

```
for col in df.select_dtypes(include=[np.number]).columns:
    if missing_percentage[col] < 10:
        df[col].fillna(df[col].mean(), inplace=True)

```

-   `select_dtypes` filters numeric columns.

-   We check if missing percentage is less than 10%.

-   `fillna()` replaces missing values with the mean.

* * * * *

✅ **3\. Mode imputation for categorical data**
----------------------------------------------

**Concept**: In categorical columns (like 'Gender'), replacing missing values with the **mode** (most frequent value) is common.

```
for col in df.select_dtypes(include=['object']).columns:
    mode_value = df[col].mode()[0]
    df[col].fillna(mode_value, inplace=True)

```

-   `mode()` gives the most frequent value in a column.

-   `fillna(mode)` fills missing values with that frequent value.

* * * * *

✅ **4\. KNN Imputer to estimate missing values**
------------------------------------------------

**Concept**: KNN (K-Nearest Neighbors) estimates missing values based on values from the **closest rows (neighbors)**.

```
knn_imputer = KNNImputer(n_neighbors=2)
df_knn[['Age', 'Salary']] = knn_imputer.fit_transform(df_knn[['Age', 'Salary']])

```

-   `KNNImputer` finds the average value from `n_neighbors` closest rows for each missing value.

-   It works **only on numeric columns**.

* * * * *

✅ **5\. Drop columns with >10% missing values**
-----------------------------------------------

**Concept**: If a column has too many missing values (more than 10%), it may not be useful, so we **drop it**.

```
df_cleaned = df.dropna(thresh=len(df) * 0.9, axis=1)

```

-   `thresh=len(df)*0.9` keeps only columns with at least 90% non-null values.

-   `axis=1` means we're checking columns (use `axis=0` for rows).

* * * * *

✅ **6\. Drop rows with Z-score > 3 (Outliers)**
-----------------------------------------------

**Concept**: A **Z-score** > 3 usually means a value is too far from the mean---called an outlier. We remove such rows.

```
z_scores = np.abs(zscore(df_cleaned.select_dtypes(include=[np.number])))
df_no_outliers = df_cleaned[(z_scores < 3).all(axis=1)]

```

-   `zscore()` calculates how far each value is from the mean.

-   Rows where **all** values have `z < 3` are kept.

* * * * *

✅ **7\. Drop duplicate rows based on 50% similar columns**
----------------------------------------------------------

**Concept**: Sometimes rows are **partially duplicated** (e.g., half the columns are the same). We want to remove them.

```
threshold = df.shape[1] // 2
df_nodups = df[~df.duplicated(subset=df.columns[:threshold])]

```

-   `df.shape[1]` is number of columns.

-   `duplicated()` checks if the first half of columns match in other rows.

-   `~` negates it, so we **keep** only non-duplicates.

* * * * *

✅ **8\. Min-Max Normalization**
-------------------------------

**Concept**: **Rescaling** values to a fixed range (usually 0 to 1) helps machine learning models perform better.

```
scaler = MinMaxScaler()
df_scaled['Salary'] = scaler.fit_transform(df[['Salary']])

```

-   `MinMaxScaler()` transforms each value using:

    Xscaled=X-Xmin⁡Xmax⁡-Xmin⁡X_{\text{scaled}} = \frac{X - X_{\min}}{X_{\max} - X_{\min}}

* * * * *

✅ **9\. Binarize data**
-----------------------

**Concept**: Converts numeric values to 0 or 1 based on a **threshold**.

```
binarizer = Binarizer(threshold=60000)
df_binarized['Salary_bin'] = binarizer.fit_transform(df[['Salary']])

```

-   Values **> 60000** become 1; others become 0.

-   Useful when you want to create a binary target variable.

* * * * *

✅ **10\. One-Hot Encoding for categorical feature**
---------------------------------------------------

**Concept**: Converts a categorical column (like `Department`) into **multiple binary columns**.

```
df_encoded = pd.get_dummies(df, columns=['Department'])

```

-   `'HR'`, `'IT'`, `'Finance'` become columns like:\
    `Department_HR`, `Department_IT`, `Department_Finance`

-   Only **one column is 1** for each row; others are 0.

* * * * *

## CheatSheet


### 🧾 **Machine Learning Preprocessing Cheatsheet (Python)**

| **Task** | **Purpose** | **Syntax** |
| --- | --- | --- |
| **1\. Missing % in columns** | Check missing value percentage | `df.isnull().mean() * 100` |
| **2\. Replace missing (mean)** | Fill numeric missing values if % < 10 | `df[col].fillna(df[col].mean(), inplace=True)` |
| **3\. Replace missing (mode)** | Fill categorical missing values | `df[col].fillna(df[col].mode()[0], inplace=True)` |
| **4\. KNN Imputer** | Estimate missing values using KNN | `KNNImputer(n_neighbors=2).fit_transform(df[['col1', 'col2']])` |
| **5\. Drop columns with >10% missing** | Remove columns with many nulls | `df.dropna(thresh=len(df) * 0.9, axis=1)` |
| **6\. Drop outliers (Z-score > 3)** | Remove outlier rows | `zscore(df_numeric)`, then `df[(z_scores < 3).all(axis=1)]` |
| **7\. Drop semi-duplicates** | Remove rows where 50% columns match | `df[~df.duplicated(subset=df.columns[:half])` |
| **8\. Min-Max Normalization** | Scale values between 0 and 1 | `MinMaxScaler().fit_transform(df[['col']])` |
| **9\. Binarize data** | Convert numeric to 0/1 | `Binarizer(threshold=val).fit_transform(df[['col']])` |
| **10\. One-Hot Encoding** | Encode categorical to binary columns | `pd.get_dummies(df, columns=['cat_col'])` |

* * * * *

### 🔧 **Imports You'll Need**

Make sure to import these libraries at the top of your script:

```
import pandas as pd
import numpy as np
from sklearn.impute import KNNImputer
from sklearn.preprocessing import MinMaxScaler, Binarizer
from scipy.stats import zscore

```

* * * * *
Made with by Ronnie Allen