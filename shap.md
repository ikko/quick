### **SHAP (SHapley Additive exPlanations) Cheatsheet**  
**SHAP** is a Python library for explaining machine learning models' predictions based on **Shapley values**, which come from game theory. SHAP provides interpretable and theoretically grounded explanations for feature contributions.

---

## **1. Installation**

Install the SHAP package via pip:
```bash
pip install shap
```

---

## **2. Key Concepts**

- **Shapley Value**: Measures the average contribution of a feature to predictions by considering all possible feature combinations.  
- **SHAP Values**: A decomposition of predictions into contributions by each feature.  
- **Interpretability**: SHAP values are consistent, local, and model-agnostic.

### Types of SHAP Explainers:
1. **TreeExplainer**: Optimized for tree-based models (e.g., XGBoost, LightGBM, RandomForest).  
2. **KernelExplainer**: Model-agnostic, works for any model but slower.  
3. **LinearExplainer**: For linear models.  
4. **DeepExplainer**: For deep learning models (e.g., TensorFlow/Keras).  
5. **GradientExplainer**: For models with gradient information.  

---

## **3. Basic SHAP Workflow**

### Step 1: Import SHAP and train a model
```python
import shap
import xgboost
import pandas as pd

# Load data
X_train, y_train = shap.datasets.boston()

# Train an XGBoost model
model = xgboost.XGBRegressor().fit(X_train, y_train)
```

### Step 2: Select an Explainer
Choose the appropriate explainer based on your model type:
```python
explainer = shap.TreeExplainer(model)  # For tree-based models
```

### Step 3: Calculate SHAP Values
```python
shap_values = explainer.shap_values(X_train)
```

### Step 4: Visualization of SHAP Values
```python
shap.summary_plot(shap_values, X_train)  # Summary plot
```

---

## **4. SHAP Explainers**

### **TreeExplainer**
- Optimized for **tree-based models**.
- Fast and accurate for models like XGBoost, LightGBM, and RandomForest.

```python
import shap

explainer = shap.TreeExplainer(model)
shap_values = explainer.shap_values(X_train)
shap.summary_plot(shap_values, X_train)
```

### **KernelExplainer**
- Model-agnostic (works for any model), but computationally expensive.

```python
import shap
import numpy as np

# Model predictions
def model_predict(data):
    return model.predict(data)

# Kernel Explainer
explainer = shap.KernelExplainer(model_predict, X_train.sample(50))
shap_values = explainer.shap_values(X_train)

shap.summary_plot(shap_values, X_train)
```

### **LinearExplainer**
- For linear models (e.g., LinearRegression).

```python
from sklearn.linear_model import LinearRegression

# Train a linear model
linear_model = LinearRegression().fit(X_train, y_train)

# Linear Explainer
explainer = shap.LinearExplainer(linear_model, X_train)
shap_values = explainer.shap_values(X_train)

shap.summary_plot(shap_values, X_train)
```

### **DeepExplainer**
- For deep learning models using frameworks like Keras or TensorFlow.

```python
import shap
import tensorflow as tf
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense

# Define and train a simple neural network
model = Sequential([Dense(10, activation='relu', input_shape=(X_train.shape[1],)), Dense(1)])
model.compile(optimizer='adam', loss='mse')
model.fit(X_train, y_train, epochs=10, verbose=0)

# Deep Explainer
explainer = shap.DeepExplainer(model, X_train[:100])
shap_values = explainer.shap_values(X_train[:100])

shap.summary_plot(shap_values, X_train[:100])
```

---

## **5. Visualization**

### **Summary Plot**
A global view of feature importance and direction of influence.
```python
shap.summary_plot(shap_values, X_train)
```

### **Dependence Plot**
Shows how a feature's value impacts the prediction.
```python
shap.dependence_plot("RM", shap_values, X_train)
```

### **Partial Dependence Plot**
Shows one feature (here `age`) dependence, keeps other features constant
```python
shap.partial_dependence_plot("age", model.predict, X)

### **Force Plot**
Visualizes individual predictions and feature contributions.
```python
shap.initjs()  # For Jupyter Notebook
shap.force_plot(explainer.expected_value, shap_values[0], X_train.iloc[0])
```

### **Waterfall Plot**
Explains how each feature contributes to a single prediction.
```python
shap.plots.waterfall(shap_values[0])
```

### **Decision Plot**
Shows how features contribute cumulatively to a prediction.
```python
shap.decision_plot(explainer.expected_value, shap_values, X_train)
```

---

## **6. SHAP for Model Debugging**

### Identify Overfitting or Feature Bias  
- If **irrelevant features** have high SHAP values, the model might have learned noise.

### Feature Importance Ranking  
- Use SHAP values to rank features by importance.  
```python
shap.summary_plot(shap_values, X_train)
```

---

## **7. Example: End-to-End Workflow**

```python
import shap
import xgboost
import pandas as pd

# Load the data
X_train, y_train = shap.datasets.boston()

# Train a model
model = xgboost.XGBRegressor().fit(X_train, y_train)

# SHAP Explainer
explainer = shap.TreeExplainer(model)
shap_values = explainer.shap_values(X_train)

# Summary Plot
shap.summary_plot(shap_values, X_train)

# Dependence Plot
shap.dependence_plot("RM", shap_values, X_train)

# Force Plot (single prediction)
shap.initjs()
shap.force_plot(explainer.expected_value, shap_values[0], X_train.iloc[0])
```

---

## **8. Useful Tips**

- **Model-Agnostic SHAP**: Use `KernelExplainer` for models that SHAP does not natively support.  
- **SHAP in Large Datasets**: Use subsets of the data to reduce computation time.  
- **Explain a Single Prediction**: Use `force_plot` for local explanations.

---

## **9. Common Visualizations**

| **Plot**           | **Use Case**                                             |
|---------------------|---------------------------------------------------------|
| **Summary Plot**    | Global feature importance and SHAP value distributions  |
| **Dependence Plot** | Feature interaction and individual effect visualization |
| **Force Plot**      | Local explanation for a single prediction              |
| **Waterfall Plot**  | Detailed breakdown of a single prediction's SHAP values |
| **Decision Plot**   | Cumulative SHAP contributions across features          |

---

## **10. Resources**  

- **Official Documentation**: [https://shap.readthedocs.io/](https://shap.readthedocs.io/)  
- **GitHub Repository**: [https://github.com/slundberg/shap](https://github.com/slundberg/shap)  

---

This cheatsheet provides a quick overview of SHAP's key features, explainers, and visualizations to interpret machine learning models effectively.
