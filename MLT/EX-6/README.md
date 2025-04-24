# Exercise 6: Backpropagation Algorithm for Training MLP using Scikit-learn or TensorFlow

## 🔧 **1. Data Preprocessing and Normalization**

```python
import pandas as pd
from sklearn.preprocessing import MinMaxScaler

# Load dataset
df = pd.read_csv("data.csv")

# Fill missing values
df.fillna(df.mean(numeric_only=True), inplace=True)

# Normalize numerical features
scaler = MinMaxScaler()
df[df.select_dtypes(include='number').columns] = scaler.fit_transform(df.select_dtypes(include='number'))
```

### ✅ Explanation:
- `fillna(df.mean())`: Fills missing values with column mean (only for numeric data).
- `MinMaxScaler()`: Scales data to a 0-1 range. Important for MLPs to converge faster.

---

## 🧩 **2. Encoding Categorical Features**

```python
from sklearn.preprocessing import OneHotEncoder

# One-hot encoding using pandas
df = pd.get_dummies(df, drop_first=True)
```

### ✅ Explanation:
- Converts categorical variables into numerical binary columns.
- `drop_first=True`: Avoids dummy variable trap (redundant column).

---

## 🧠 **3. Implement MLP with Backpropagation + Activation Functions**

```python
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense
from tensorflow.keras.utils import to_categorical
from sklearn.model_selection import train_test_split

# Example: Classification task
X = df.drop("target", axis=1)
y = to_categorical(df["target"])  # one-hot encode labels

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

# Try different activation functions
activations = ['relu', 'sigmoid', 'tanh']
for act in activations:
    print(f"Training with activation: {act}")
    model = Sequential([
        Dense(64, activation=act, input_shape=(X.shape[1],)),
        Dense(32, activation=act),
        Dense(y.shape[1], activation='softmax')  # For multi-class classification
    ])
    model.compile(optimizer='adam', loss='categorical_crossentropy', metrics=['accuracy'])
    model.fit(X_train, y_train, epochs=20, verbose=0)
    _, acc = model.evaluate(X_test, y_test, verbose=0)
    print(f"Accuracy with {act}: {acc:.4f}")
```

---

## 🛠️ **4. Hyperparameter Tuning Example**

```python
from tensorflow.keras.optimizers import Adam

model = Sequential([
    Dense(128, activation='relu'),
    Dense(64, activation='relu'),
    Dense(y.shape[1], activation='softmax')
])
optimizer = Adam(learning_rate=0.001)  # Tune this rate
model.compile(optimizer=optimizer, loss='categorical_crossentropy', metrics=['accuracy'])
model.fit(X_train, y_train, epochs=50, batch_size=32)
```

### 🔍 Hyperparameters to tune:
- **Learning rate**: Try `0.01`, `0.001`, `0.0001`
- **Batch size**: Common: `16`, `32`, `64`
- **Hidden layers/neurons**: `64`, `128`, etc.
- **Epochs**: `10–100` depending on convergence

---

## ⚙️ **5. Compare Optimizers**

```python
from tensorflow.keras.optimizers import SGD, RMSprop, Adam, Adagrad

optimizers = {
    'SGD': SGD(),
    'RMSprop': RMSprop(),
    'Adam': Adam(),
    'Adagrad': Adagrad()
}

for name, opt in optimizers.items():
    print(f"Using Optimizer: {name}")
    model = Sequential([
        Dense(64, activation='relu'),
        Dense(32, activation='relu'),
        Dense(y.shape[1], activation='softmax')
    ])
    model.compile(optimizer=opt, loss='categorical_crossentropy', metrics=['accuracy'])
    model.fit(X_train, y_train, epochs=20, verbose=0)
    _, acc = model.evaluate(X_test, y_test, verbose=0)
    print(f"Accuracy with {name}: {acc:.4f}")
```

---

## ⚡ Activation Functions – Detailed Explanation

| **Name**     | **Formula**                             | **Use Case**                          | **Pros**                                  | **Cons**                                      |
|--------------|------------------------------------------|----------------------------------------|--------------------------------------------|-----------------------------------------------|
| **Sigmoid**  | \( \frac{1}{1 + e^{-x}} \)               | Binary classification (output layer)  | Smooth curve, output in (0,1)              | Vanishing gradient, slow learning             |
| **Tanh**     | \( \frac{e^x - e^{-x}}{e^x + e^{-x}} \)  | Hidden layers (alternative to sigmoid) | Zero-centered, better than sigmoid         | Vanishing gradient                            |
| **ReLU**     | \( \max(0, x) \)                         | Hidden layers (default choice)         | Fast, sparse activation, avoids vanishing  | Dying ReLU problem (zeros output for <0 input)|
| **Leaky ReLU** | \( \max(0.01x, x) \)                   | Alternative to ReLU                    | Solves dead neuron problem                 | Slightly slower than ReLU                     |
| **Softmax**  | \( \frac{e^{x_i}}{\sum_j e^{x_j}} \)     | Output layer (multi-class classification) | Converts to probability distribution    | Not for hidden layers                         |

---

## 📌 MLP + Backpropagation Cheat Sheet

| **Step**                              | **Function**                                      | **Explanation**                                                   |
|---------------------------------------|--------------------------------------------------|-------------------------------------------------------------------|
| Data Loading                          | `pd.read_csv()`                                  | Reads dataset into DataFrame                                     |
| Fill Missing Values                   | `df.fillna(df.mean())`                           | Fills missing with column mean                                   |
| Normalize                             | `MinMaxScaler()`                                 | Scales features to 0-1                                           |
| Encode Categorical                    | `pd.get_dummies()`                               | One-hot encodes string categories                                |
| Create Model                          | `Sequential([...])`                              | Stacks MLP layers                                                |
| Compile                               | `model.compile(optimizer, loss, metrics)`        | Set loss function & optimization strategy                        |
| Train Model                           | `model.fit(X_train, y_train, epochs=...)`        | Trains the model using backpropagation                          |
| Evaluate Model                        | `model.evaluate(X_test, y_test)`                 | Returns test loss & accuracy                                     |
| Try Activation Functions              | `'relu'`, `'sigmoid'`, `'tanh'`                  | Experiment with layer-wise activations                          |
| Try Optimizers                        | `SGD()`, `Adam()`, etc.                          | Improve training convergence                                    |

---
Made with By Ronnie Allen