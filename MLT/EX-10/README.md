# Exercise 3 on Univariate Plots for Data Exploration using Matplotlib and Seaborn

### **1. Score Distribution Analysis**

This task focuses on analyzing the distribution of scores across subjects like **Math**, **Reading**, and **Writing**. The goal is to visualize how scores are distributed, and summarize key statistics such as mean, median, and standard deviation.

#### **Code for Score Distribution Analysis**

```python
import matplotlib.pyplot as plt
import seaborn as sns
import pandas as pd

# Load a sample dataset (you can replace this with your own data)
data = pd.read_csv("student_scores.csv")

# Plotting Histograms with KDE for Math, Reading, and Writing scores
plt.figure(figsize=(12, 8))

# Math scores distribution
plt.subplot(2, 2, 1)
sns.histplot(data['Math'], kde=True, color='blue')
plt.title('Math Score Distribution')

# Reading scores distribution
plt.subplot(2, 2, 2)
sns.histplot(data['Reading'], kde=True, color='green')
plt.title('Reading Score Distribution')

# Writing scores distribution
plt.subplot(2, 2, 3)
sns.histplot(data['Writing'], kde=True, color='red')
plt.title('Writing Score Distribution')

plt.tight_layout()
plt.show()

# Summary Statistics
print("Math Score Statistics:")
print(data['Math'].describe())
print("\nReading Score Statistics:")
print(data['Reading'].describe())
print("\nWriting Score Statistics:")
print(data['Writing'].describe())
```

#### **Explanation**:
- **Histograms with KDE (Kernel Density Estimation)**: We use `sns.histplot()` to plot histograms and overlay KDE plots for each score distribution (Math, Reading, Writing).
- **Summary Statistics**: `describe()` function provides summary statistics for each subject, including mean, median, standard deviation, minimum, and maximum values.

#### **Insights**:
- **Shape of Distributions**: The histograms will help identify whether the distribution is normal, skewed, or bimodal.
- **Patterns**: Patterns in the score distributions (e.g., clusters, outliers) will be visible through the KDE plots.

---

### **2. Study Hours Analysis**

This task focuses on visualizing the relationship between study hours and academic performance using box plots and violin plots. Additionally, correlations between study hours and subject scores will be computed.

#### **Code for Study Hours Analysis**

```python
# Study Hours vs Scores Visualization
plt.figure(figsize=(10, 6))

# Box Plot of Study Hours vs Math Scores
plt.subplot(1, 2, 1)
sns.boxplot(x=data['StudyHours'], y=data['Math'])
plt.title('Box Plot: Study Hours vs Math Scores')

# Violin Plot of Study Hours vs Reading Scores
plt.subplot(1, 2, 2)
sns.violinplot(x=data['StudyHours'], y=data['Reading'])
plt.title('Violin Plot: Study Hours vs Reading Scores')

plt.tight_layout()
plt.show()

# Correlation Calculation between Study Hours and Scores
study_hours_corr = data[['StudyHours', 'Math', 'Reading', 'Writing']].corr()
print("Correlation between Study Hours and Scores:")
print(study_hours_corr)
```

#### **Explanation**:
- **Box Plot**: `sns.boxplot()` visualizes the distribution of Math scores against different study hours, showing outliers, quartiles, and median values.
- **Violin Plot**: `sns.violinplot()` is similar to a box plot but shows the distribution shape. It gives insights into the density and variation of the data.
- **Correlation**: The `.corr()` function calculates the correlation between study hours and the different subjects' scores, helping to determine any linear relationship.

#### **Insights**:
- **Patterns**: The box plot helps identify outliers or any skewness in study hours that could impact scores.
- **Correlation**: A strong positive correlation between study hours and scores would indicate a direct relationship, where more study hours may result in better academic performance.

---

### **3. Sleep Patterns Analysis**

This task investigates the relationship between sleep duration and academic performance. We will visualize sleep duration using density plots, group students by their sleep hours, and analyze their performance.

#### **Code for Sleep Patterns Analysis**

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

#### **Explanation**:
- **Density Plot**: `sns.kdeplot()` creates a density plot to show the distribution of sleep hours across students.
- **Sleep Grouping**: `pd.cut()` segments students into different sleep duration groups.
- **Box Plot**: We use `sns.boxplot()` to compare writing scores across different sleep groups.
- **Performance Analysis**: Grouping by sleep duration helps us understand if there’s any significant performance difference between students with different sleep patterns.

#### **Insights**:
- **Optimal Sleep Pattern**: Box plots and summary statistics will reveal whether sleep patterns (e.g., 6-8 hours) are associated with higher scores.
- **Relationships**: The density plot helps visualize the overall sleep behavior, and the group-wise performance analysis highlights how sleep hours impact performance.

---

### **Summary of Visualizations and Insights**

1. **Score Distribution Analysis**:
   - The distribution of scores can highlight how well students perform in each subject.
   - KDE plots provide smooth distributions, making it easier to identify skewness or other patterns.

2. **Study Hours Analysis**:
   - Box plots help identify the spread of scores for different study hours and identify outliers.
   - Violin plots are useful for understanding the density and spread of scores across study hours.
   - Correlations provide a numerical measure of the relationship between study hours and academic performance.

3. **Sleep Patterns Analysis**:
   - The density plot shows the overall sleep distribution, while box plots provide a way to compare sleep groups with performance.
   - Grouped data allows us to analyze how students with varying sleep durations perform in different subjects.

---
Made with by Ronnie Allen