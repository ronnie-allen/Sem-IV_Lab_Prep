# EX-3: Univariate Plots for Data Exploration using Matplotlib and Seaborn
---

## **Cheat Sheet for Univariate Plots with Matplotlib & Seaborn**

### **1. Plotting with Seaborn and Matplotlib**

- **Seaborn (`sns`)**: High-level interface for drawing attractive statistical graphics.
- **Matplotlib (`plt`)**: Low-level library for creating static, animated, and interactive visualizations.

#### **Key Seaborn Functions**

- **`sns.histplot()`**: Plot a histogram with an optional Kernel Density Estimation (KDE).
  ```python
  sns.histplot(data['column'], kde=True)
  ```

- **`sns.boxplot()`**: Plot a box plot for visualizing the distribution of a variable.
  ```python
  sns.boxplot(x=data['column'])
  ```

- **`sns.violinplot()`**: Combine aspects of box plot and KDE plot for showing distributions.
  ```python
  sns.violinplot(x=data['column'])
  ```

- **`sns.kdeplot()`**: Plot a smooth curve (KDE) for the distribution of a continuous variable.
  ```python
  sns.kdeplot(data['column'], shade=True)
  ```

#### **Key Matplotlib Functions**

- **`plt.figure()`**: Create a new figure.
  ```python
  plt.figure(figsize=(10, 6))
  ```

- **`plt.subplot()`**: Create subplots within a single figure.
  ```python
  plt.subplot(2, 2, 1)
  ```

- **`plt.show()`**: Display the plot.
  ```python
  plt.show()
  ```

---

### **2. Statistical Summary Functions**

- **`data.describe()`**: Provides summary statistics (mean, median, standard deviation) for numerical columns.
  ```python
  data['column'].describe()
  ```

- **`data.corr()`**: Compute pairwise correlation between variables.
  ```python
  data[['col1', 'col2']].corr()
  ```

---

### **3. Creating Univariate Plots for Data Analysis**

#### **Score Distribution Analysis**

- **Histograms and KDE**: To understand the shape of the distribution for Math, Reading, and Writing scores.
  ```python
  sns.histplot(data['Math'], kde=True)
  sns.histplot(data['Reading'], kde=True)
  sns.histplot(data['Writing'], kde=True)
  ```

#### **Study Hours Analysis**

- **Box Plot**: Helps visualize the distribution of scores across study hours.
  ```python
  sns.boxplot(x=data['StudyHours'], y=data['Math'])
  ```

- **Violin Plot**: Visualize the density of scores across study hours.
  ```python
  sns.violinplot(x=data['StudyHours'], y=data['Reading'])
  ```

- **Correlation**: To calculate the relationship between study hours and scores.
  ```python
  data[['StudyHours', 'Math', 'Reading']].corr()
  ```

#### **Sleep Patterns Analysis**

- **Density Plot**: Visualizes the distribution of sleep hours.
  ```python
  sns.kdeplot(data['SleepHours'], shade=True)
  ```

- **Box Plot for Sleep Group vs. Scores**: Comparing the effect of sleep on academic performance.
  ```python
  sns.boxplot(x=data['SleepGroup'], y=data['Writing'])
  ```

- **Grouping Data**: Use `pd.cut()` to segment data into different groups based on sleep hours.
  ```python
  sleep_groups = pd.cut(data['SleepHours'], bins=[0, 4, 6, 8, 10, 12], labels=['0-4', '4-6', '6-8', '8-10', '10-12'])
  data['SleepGroup'] = sleep_groups
  ```

---

### **4. Example Code for Visualization**

#### **1. Score Distribution Analysis**

```python
# Histograms with KDE
plt.figure(figsize=(12, 8))
plt.subplot(2, 2, 1)
sns.histplot(data['Math'], kde=True, color='blue')
plt.title('Math Score Distribution')

plt.subplot(2, 2, 2)
sns.histplot(data['Reading'], kde=True, color='green')
plt.title('Reading Score Distribution')

plt.subplot(2, 2, 3)
sns.histplot(data['Writing'], kde=True, color='red')
plt.title('Writing Score Distribution')

plt.tight_layout()
plt.show()

# Summary Statistics
print(data['Math'].describe())
print(data['Reading'].describe())
print(data['Writing'].describe())
```

#### **2. Study Hours Analysis**

```python
# Box Plot and Violin Plot for Study Hours vs Scores
plt.figure(figsize=(10, 6))

plt.subplot(1, 2, 1)
sns.boxplot(x=data['StudyHours'], y=data['Math'])
plt.title('Box Plot: Study Hours vs Math Scores')

plt.subplot(1, 2, 2)
sns.violinplot(x=data['StudyHours'], y=data['Reading'])
plt.title('Violin Plot: Study Hours vs Reading Scores')

plt.tight_layout()
plt.show()

# Correlation between Study Hours and Scores
study_hours_corr = data[['StudyHours', 'Math', 'Reading', 'Writing']].corr()
print("Correlation between Study Hours and Scores:")
print(study_hours_corr)
```

#### **3. Sleep Patterns Analysis**

```python
# Density Plot of Sleep Hours
plt.figure(figsize=(8, 6))
sns.kdeplot(data['SleepHours'], shade=True, color='purple')
plt.title('Density Plot of Sleep Hours')
plt.xlabel('Sleep Hours')
plt.ylabel('Density')
plt.show()

# Grouping students by sleep duration and analyzing performance
sleep_groups = pd.cut(data['SleepHours'], bins=[0, 4, 6, 8, 10, 12], labels=['0-4', '4-6', '6-8', '8-10', '10-12'])
data['SleepGroup'] = sleep_groups

# Box plot of Sleep Group vs Writing Scores
plt.figure(figsize=(10, 6))
sns.boxplot(x=data['SleepGroup'], y=data['Writing'], palette="Set2")
plt.title('Sleep Group vs Writing Scores')
plt.show()

# Analyzing performance of each sleep group
sleep_performance = data.groupby('SleepGroup')['Writing'].describe()
print("Sleep Group Performance Analysis:")
print(sleep_performance)
```

---

### **5. Summary of Key Insights**

- **Histograms and KDE**: These plots help in understanding the distribution of scores for different subjects.
- **Box Plots and Violin Plots**: Visualize the spread of scores and help detect outliers or extreme values.
- **Density Plots**: Ideal for understanding the continuous distribution of variables like sleep hours.
- **Correlation Analysis**: Helps quantify the relationship between variables (e.g., study hours and academic performance).

---

This **cheat sheet** and explanation will help you efficiently create and analyze visualizations using **Matplotlib** and **Seaborn** to explore univariate data. Feel free to use the code snippets to perform these tasks on your dataset and extract insights!
