# Exercise 5: Single-Layer Neural Network Using TensorFlow

**Exercise 5: Single-Layer Neural Network Using TensorFlow** --- **with code snippets and detailed explanations** for each task, including both classification and regression, activation function comparisons, and learning rate optimization.

* * * * *

🧠 1. **Single-Layer Neural Network for Classification**
--------------------------------------------------------

### 🔸 Code Snippet:

```
import tensorflow as tf
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.metrics import classification_report
import pandas as pd

# Load dataset
data = pd.read_csv("classification_data.csv")  # 1️⃣ Load your dataset
X = data.drop("label", axis=1)                 # 2️⃣ Features
y = data["label"]                              # 3️⃣ Target

# Train-Test Split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Feature Scaling
scaler = StandardScaler()
X_train = scaler.fit_transform(X_train)
X_test = scaler.transform(X_test)

# Build Model
model = tf.keras.models.Sequential([
    tf.keras.layers.Dense(1, activation='sigmoid', input_shape=(X_train.shape[1],))  # 4️⃣ Single neuron with sigmoid
])

# Compile Model
model.compile(optimizer='adam', loss='binary_crossentropy', metrics=['accuracy'])   # 5️⃣ Set optimizer, loss, metrics

# Train Model
model.fit(X_train, y_train, epochs=50, verbose=1)  # 6️⃣ Train over 50 epochs

# Evaluate
y_pred = (model.predict(X_test) > 0.5).astype(int)  # 7️⃣ Predict class (binary)
print(classification_report(y_test, y_pred))        # 8️⃣ Evaluate with accuracy, precision, recall

```

* * * * *

🧠 2. **Single-Layer Neural Network for Regression**
----------------------------------------------------

### 🔸 Code Snippet:

```
from sklearn.metrics import mean_squared_error, mean_absolute_error

# Load data
data = pd.read_csv("regression_data.csv")
X = data.drop("target", axis=1)
y = data["target"]

# Split & Scale
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)
X_train = scaler.fit_transform(X_train)
X_test = scaler.transform(X_test)

# Build regression model
model = tf.keras.models.Sequential([
    tf.keras.layers.Dense(1, activation='linear', input_shape=(X_train.shape[1],))  # 1️⃣ Linear activation for regression
])

# Compile & Train
model.compile(optimizer='adam', loss='mse')  # 2️⃣ MSE is a good regression loss
model.fit(X_train, y_train, epochs=50)

# Evaluate
preds = model.predict(X_test)
print("MSE:", mean_squared_error(y_test, preds))  # 3️⃣ Mean Squared Error
print("MAE:", mean_absolute_error(y_test, preds)) # 4️⃣ Mean Absolute Error

```

* * * * *

🧠 3. **Activation Function Comparison**
----------------------------------------

### 🔸 Code Snippet:

```
activations = ['sigmoid', 'relu', 'tanh']  # 1️⃣ Different activation functions

for act in activations:
    print(f"Using activation: {act}")
    model = tf.keras.models.Sequential([
        tf.keras.layers.Dense(1, activation=act, input_shape=(X_train.shape[1],))  # 2️⃣ Change activation here
    ])
    model.compile(optimizer='adam', loss='binary_crossentropy', metrics=['accuracy'])
    model.fit(X_train, y_train, epochs=50, verbose=0)
    print("Accuracy:", model.evaluate(X_test, y_test)[1])  # 3️⃣ Evaluate model

```

> 🔍 **Why test activations?**: Helps understand their effect on gradient flow and model accuracy.

* * * * *

🧠 4. **Learning Rate Optimization**
------------------------------------

### 🔸 Code Snippet:

```
# Try different learning rates
for lr in [0.0001, 0.001, 0.01, 0.1]:
    print(f"\nLearning Rate: {lr}")
    optimizer = tf.keras.optimizers.Adam(learning_rate=lr)  # 1️⃣ Custom learning rate

    model = tf.keras.models.Sequential([
        tf.keras.layers.Dense(1, activation='sigmoid', input_shape=(X_train.shape[1],))  # 2️⃣ Model stays same
    ])

    model.compile(optimizer=optimizer, loss='binary_crossentropy', metrics=['accuracy'])  # 3️⃣ Use custom optimizer
    model.fit(X_train, y_train, epochs=50, verbose=0)
    loss, acc = model.evaluate(X_test, y_test, verbose=0)
    print("Accuracy:", acc)  # 4️⃣ Check which learning rate gives best performance

```

> 🧪 **Goal**: Identify the learning rate that minimizes loss and maximizes accuracy.

* * * * *

🧾 Cheat Sheet Summary Table
----------------------------

| **Task** | **Code Snippet** | **Explanation** |
| --- | --- | --- |
| Load CSV | `pd.read_csv("file.csv")` | Reads dataset into DataFrame |
| Split Data | `train_test_split(X, y)` | Splits data into training & test sets |
| Normalize | `StandardScaler()` | Scales data to mean=0, std=1 |
| Build Model | `Sequential([...])` | Creates simple feed-forward model |
| Layer | `Dense(1, activation='...')` | Single output neuron with activation |
| Compile | `model.compile(optimizer, loss)` | Configures model for training |
| Train | `model.fit(X, y, epochs=n)` | Fits the model on training data |
| Predict | `model.predict(X_test)` | Generates predictions |
| Evaluate Classification | `classification_report()` | Shows accuracy, precision, recall |
| Evaluate Regression | `mean_squared_error()` | Shows how close predictions are to true values |
| Try Activations | Loop `['sigmoid', 'relu']` | Test effect of different activation functions |
| Try Learning Rate | `Adam(learning_rate=...)` | Test convergence based on LR |

* * * * *
Made with by Ronnie Allen