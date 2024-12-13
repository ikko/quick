Here’s a **comprehensive handbook** on **Scikit-Learn (sklearn)**, the Python library for machine learning. This guide will cover key concepts, code examples, and practical use cases.

---

# **Scikit-Learn Handbook**

## **1. Introduction to Scikit-Learn**

- **Scikit-Learn**: A Python library for **machine learning** that supports:
  - **Supervised learning** (classification, regression)
  - **Unsupervised learning** (clustering, dimensionality reduction)
  - **Model selection** (cross-validation, hyperparameter tuning)
  - **Data preprocessing** (scaling, encoding, handling missing values)

### **Installation**
```bash
pip install scikit-learn
```

### **Check Version**
```python
import sklearn
print(sklearn.__version__)
```

---

## **2. Key Concepts**

- **Estimator**: A machine learning model or transformer (e.g., `LinearRegression`).
- **Fit**: Train the model using training data.
- **Predict**: Predict target values on test data.
- **Transform**: Modify data (used for preprocessing).
- **Pipeline**: Combine preprocessing steps and a model into one workflow.

---

## **3. Dataset Loading**

Scikit-Learn provides built-in datasets for experimentation.

### **Load Built-in Datasets**
```python
from sklearn.datasets import load_iris, load_digits, fetch_california_housing

# Load Iris dataset
iris = load_iris()
X, y = iris.data, iris.target  # Features and labels
print(iris.DESCR)  # Dataset description
```

### **Load External Datasets**
```python
import pandas as pd

# Load CSV data
data = pd.read_csv("data.csv")
X = data.drop(columns=["target"])
y = data["target"]
```

---

## **4. Data Preprocessing**

### **1. Handling Missing Values**
```python
from sklearn.impute import SimpleImputer
import numpy as np

imputer = SimpleImputer(strategy="mean")
X = np.array([[1, 2, np.nan], [3, np.nan, 4]])
X_imputed = imputer.fit_transform(X)
```

### **2. Feature Scaling**
```python
from sklearn.preprocessing import StandardScaler, MinMaxScaler

scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)
```

### **3. Encoding Categorical Variables**
```python
from sklearn.preprocessing import OneHotEncoder

encoder = OneHotEncoder(sparse=False)
X_categorical = [["Red"], ["Green"], ["Blue"]]
X_encoded = encoder.fit_transform(X_categorical)
```

### **4. Train-Test Split**
```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
```

---

## **5. Supervised Learning**

### **1. Regression**

#### **Linear Regression**
```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error

# Train the model
model = LinearRegression()
model.fit(X_train, y_train)

# Predict and evaluate
y_pred = model.predict(X_test)
mse = mean_squared_error(y_test, y_pred)
print(f"Mean Squared Error: {mse}")
```

#### **Decision Tree Regression**
```python
from sklearn.tree import DecisionTreeRegressor

tree = DecisionTreeRegressor(max_depth=5)
tree.fit(X_train, y_train)
```

---

### **2. Classification**

#### **Logistic Regression**
```python
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score

log_reg = LogisticRegression()
log_reg.fit(X_train, y_train)
y_pred = log_reg.predict(X_test)

# Evaluate accuracy
print("Accuracy:", accuracy_score(y_test, y_pred))
```

#### **Random Forest Classifier**
```python
from sklearn.ensemble import RandomForestClassifier

rf = RandomForestClassifier(n_estimators=100, random_state=42)
rf.fit(X_train, y_train)
```

#### **Support Vector Machine (SVM)**
```python
from sklearn.svm import SVC

svm = SVC(kernel="linear")
svm.fit(X_train, y_train)
```

---

## **6. Unsupervised Learning**

### **1. Clustering**

#### **K-Means Clustering**
```python
from sklearn.cluster import KMeans

kmeans = KMeans(n_clusters=3, random_state=42)
kmeans.fit(X)
print(kmeans.labels_)  # Cluster labels
```

#### **DBSCAN**
```python
from sklearn.cluster import DBSCAN

dbscan = DBSCAN(eps=0.5, min_samples=5)
labels = dbscan.fit_predict(X)
```

---

### **2. Dimensionality Reduction**

#### **Principal Component Analysis (PCA)**
```python
from sklearn.decomposition import PCA

pca = PCA(n_components=2)
X_reduced = pca.fit_transform(X)
```

---

## **7. Model Evaluation**

### **Metrics**

#### **Classification Metrics**
```python
from sklearn.metrics import accuracy_score, confusion_matrix, classification_report

print(accuracy_score(y_test, y_pred))
print(confusion_matrix(y_test, y_pred))
print(classification_report(y_test, y_pred))
```

#### **Regression Metrics**
```python
from sklearn.metrics import mean_absolute_error, mean_squared_error

print(mean_absolute_error(y_test, y_pred))
print(mean_squared_error(y_test, y_pred))
```

---

### **Cross-Validation**
```python
from sklearn.model_selection import cross_val_score

scores = cross_val_score(model, X, y, cv=5, scoring="accuracy")
print("Cross-validation scores:", scores)
```

---

## **8. Hyperparameter Tuning**

### **Grid Search**
```python
from sklearn.model_selection import GridSearchCV

param_grid = {'n_estimators': [100, 200], 'max_depth': [None, 10, 20]}
grid_search = GridSearchCV(RandomForestClassifier(), param_grid, cv=5)
grid_search.fit(X_train, y_train)

print("Best Parameters:", grid_search.best_params_)
```

### **Randomized Search**
```python
from sklearn.model_selection import RandomizedSearchCV

random_search = RandomizedSearchCV(RandomForestClassifier(), param_distributions=param_grid, n_iter=10, cv=5)
random_search.fit(X_train, y_train)
```

---

## **9. Pipelines**

Combine preprocessing steps and models.

```python
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.svm import SVC

pipeline = Pipeline([
    ("scaler", StandardScaler()),
    ("svm", SVC(kernel="rbf"))
])

pipeline.fit(X_train, y_train)
y_pred = pipeline.predict(X_test)
```

---

## **10. Saving and Loading Models**

### **Save a Model**
```python
import joblib

joblib.dump(model, "model.pkl")
```

### **Load a Model**
```python
loaded_model = joblib.load("model.pkl")
y_pred = loaded_model.predict(X_test)
```

---

## **11. Scikit-Learn Extensions**

| **Extension**          | **Purpose**                                |
|-------------------------|--------------------------------------------|
| **imbalanced-learn**    | Handle imbalanced datasets                |
| **sklearn-pandas**      | DataFrames preprocessing pipelines        |
| **Feature-engine**      | Advanced feature engineering techniques   |

Install an extension:
```bash
pip install imbalanced-learn
```

---

## **12. Cheat Sheet of Common Methods**

| **Step**            | **Method**                          | **Example**                            |
|----------------------|-------------------------------------|----------------------------------------|
| Preprocessing        | `StandardScaler()`                 | `scaler.fit_transform(X)`             |
| Train-Test Split     | `train_test_split()`               | `X_train, X_test, y_train, y_test = train_test_split()`|
| Model Training       | `model.fit()`                      | `model.fit(X_train, y_train)`         |
| Prediction           | `model.predict()`                  | `model.predict(X_test)`               |
| Evaluation           | `accuracy_score()`                 | `accuracy_score(y_test, y_pred)`      |
| Cross-Validation     | `cross_val_score()`                | `cross_val_score(model, X, y)`        |
| Hyperparameter Tuning| `GridSearchCV()`                   | `GridSearchCV(estimator, params)`     |

---

## **13. Summary**

Scikit-Learn is the **go-to library** for machine learning tasks in Python, offering tools for model training, evaluation, and deployment. Mastering preprocessing, pipelines, and evaluation metrics will streamline your ML workflows.
