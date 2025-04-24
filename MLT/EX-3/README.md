# Exercise 2 -- Find-S Algorithm (Concept Learning)

### ✅ **1\. Read the training data from CSV**

```
import pandas as pd

# Load dataset
df = pd.read_csv('training_data.csv')

```

* * * * *

### ✅ **2\. Display the first and last 5 rows**

```
print(df.head())   # First 5 rows
print(df.tail())   # Last 5 rows

```

* * * * *

### ✅ **3\. Identify number of attributes and instances**

```
num_attributes = df.shape[1] - 1   # Last column is the target
num_instances = df.shape[0]

print("Number of attributes:", num_attributes)
print("Number of instances:", num_instances)

```

* * * * *

### ✅ **4\. Initialize the most specific hypothesis**

```
# Assuming all attributes are strings
hypothesis = ['0'] * num_attributes

```

-   `'0'` means "most specific" (nothing is accepted yet).

* * * * *

### ✅ **5\. FIND-S Algorithm Implementation**

```
def find_s_algorithm(data):
    attributes = data.iloc[:, :-1].values  # All rows, all columns except last
    target = data.iloc[:, -1].values       # Target values

    # Step 1: Initialize the most specific hypothesis
    hypothesis = ['0'] * attributes.shape[1]

    print("\nInitial hypothesis:", hypothesis)

    # Step 2: Iterate through training examples
    for i, instance in enumerate(attributes):
        if target[i].lower() == 'yes':  # Process only positive examples
            for j in range(len(hypothesis)):
                if hypothesis[j] == '0':               # If hypothesis is most specific, adopt attribute
                    hypothesis[j] = instance[j]
                elif hypothesis[j] != instance[j]:     # Generalize if attribute differs
                    hypothesis[j] = '?'
        print(f"After instance {i+1}: {hypothesis}")

    return hypothesis

```

* * * * *

### ✅ **6\. Display final hypothesis**

```
final_hypothesis = find_s_algorithm(df)
print("\nFinal hypothesis learned:", final_hypothesis)

```

* * * * *

### ✅ **7\. Test learned hypothesis on new instances**

```
def test_hypothesis(hypothesis, new_instance):
    for h, val in zip(hypothesis, new_instance):
        if h != '?' and h != val:
            return False
    return True

# Example
test_instance = ['Sunny', 'Warm', 'Normal', 'Strong', 'Warm', 'Same']
result = test_hypothesis(final_hypothesis, test_instance)
print("\nHypothesis result for test instance:", "Positive" if result else "Negative")

```

* * * * *

🧾 **Find-S Algorithm Cheatsheet (with Function Logic)**
--------------------------------------------------------

| **Step** | **Purpose** | **Function / Logic** | **Explanation** |
| --- | --- | --- | --- |
| Read CSV | Load training data | `pd.read_csv()` | Reads dataset into a DataFrame |
| View rows | Preview data | `df.head()`, `df.tail()` | Shows first/last rows for inspection |
| Data info | Attribute & instance count | `df.shape[0]`, `df.shape[1]` | `.shape` gives row and column count |
| Init hypothesis | Start specific | `['0'] * n` | Most specific hypothesis (nothing accepted) |
| Loop training | Go through each row | `for i, row in enumerate(data)` | Loop through dataset rows |
| Process positive | Use only positive examples | `if target[i] == 'yes'` | Only update on positive examples |
| Specific → General | Update hypothesis | `'0' → val`, `≠ → '?'` | Change from specific to more general |
| Output progress | Track learning | `print(f"After instance {i+1}")` | See how hypothesis evolves |
| Final result | Learned hypothesis | `return hypothesis` | Outputs learned concept |
| Testing | Check new example | `if h != '?' and h != val` | If mismatch, it's not classified as positive |

* * * * *

### 📌 Example Dataset (`training_data.csv`)

```
Sky,Temp,Humidity,Wind,Water,Forecast,Enjoy
Sunny,Warm,Normal,Strong,Warm,Same,Yes
Sunny,Warm,High,Strong,Warm,Same,Yes
Rainy,Cold,High,Strong,Warm,Change,No
Sunny,Warm,High,Strong,Cool,Change,Yes

```


---

## 📌 **What is Find-S Algorithm?**

Find-S is a **supervised learning algorithm** that finds the **most specific hypothesis** that fits all the **positive examples** in a dataset.

- It **ignores negative examples**.
- It starts with the most specific hypothesis and **generalizes it only when needed**.

---

## 🔍 **Code Breakdown & Explanation**

### 🔹 Step 1: Import and Load the Dataset
```python
import pandas as pd
df = pd.read_csv('training_data.csv')
```
- We import `pandas` for data handling.
- `pd.read_csv()` loads the dataset into a DataFrame.

---

### 🔹 Step 2: Create the Find-S Function
```python
def find_s_algorithm(data):
```
- This function takes the **training data** as input.

---

### 🔹 Step 3: Split Data into Attributes and Target
```python
attributes = data.iloc[:, :-1].values
target = data.iloc[:, -1].values
```
- `attributes`: All columns **except the last** (input features).
- `target`: The **last column** (class label, e.g., Yes/No).

---

### 🔹 Step 4: Initialize the Most Specific Hypothesis
```python
hypothesis = ['0'] * attributes.shape[1]
```
- Starts with the most specific hypothesis like:  
  `['0', '0', '0', '0', '0', '0']`  
- `'0'` means: no generalization yet — the hypothesis **rejects all**.

---

### 🔹 Step 5: Loop Through the Training Instances
```python
for i, instance in enumerate(attributes):
    if target[i].lower() == 'yes':
        ...
```
- Loop through each training instance.
- Process **only positive examples** (`'yes'` class).

---

### 🔹 Step 6: Update the Hypothesis
```python
for j in range(len(hypothesis)):
    if hypothesis[j] == '0':
        hypothesis[j] = instance[j]
    elif hypothesis[j] != instance[j]:
        hypothesis[j] = '?'
```

#### 👉 Logic:
- **If hypothesis value is '0'**, replace it with the current instance value.
- **If there’s a mismatch**, generalize with `'?'`.

#### Example:
If current hypothesis is  
`['Sunny', 'Warm', 'Normal', 'Strong', 'Warm', 'Same']`  
and the new instance is  
`['Sunny', 'Warm', 'High', 'Strong', 'Warm', 'Same']`

Then `'Normal'` vs `'High'` → mismatch → change to `'?'`

Updated:  
`['Sunny', 'Warm', '?', 'Strong', 'Warm', 'Same']`

---

### 🔹 Step 7: Show Intermediate Hypothesis
```python
print(f"After instance {i+1}: {hypothesis}")
```
- Displays hypothesis after each positive example is processed.

---

### 🔹 Step 8: Return Final Hypothesis
```python
return hypothesis
```
- After looping through all examples, we return the **learned hypothesis**.

---

## 🧪 Testing the Hypothesis
```python
def test_hypothesis(hypothesis, new_instance):
    for h, val in zip(hypothesis, new_instance):
        if h != '?' and h != val:
            return False
    return True
```

### 👉 Logic:
- For each attribute:
  - If hypothesis says `'Sunny'`, and input is `'Rainy'` → Reject.
  - If hypothesis says `'?'`, accept anything.
- If all attributes **match or are '?'**, return **True** (positive match).

---

## ✅ Final Example Output

Given this dataset:
```csv
Sunny,Warm,Normal,Strong,Warm,Same,Yes
Sunny,Warm,High,Strong,Warm,Same,Yes
Rainy,Cold,High,Strong,Warm,Change,No
Sunny,Warm,High,Strong,Cool,Change,Yes
```

The final hypothesis will be:
```python
['Sunny', 'Warm', '?', 'Strong', '?', '?']
```

### ✨ Meaning:
This hypothesis accepts:
- **Sunny** days
- **Warm** temperature
- Any humidity
- **Strong** wind
- Any water
- Any forecast

---

## 🎯 Summary Table

| Part | What It Does | Why It Matters |
|------|---------------|----------------|
| `'0'` | Most specific start | Rejects everything |
| `'Sunny'` or any value | Accepted value | Matched from positive example |
| `'?'` | Generalized value | Allowed due to mismatch in positive examples |
| Only 'Yes' examples used | Ignores noise | Focuses only on what makes it positive |
| `test_hypothesis()` | Matches unseen data | Used to classify new instances |

---

Made with by Ronnie Allen