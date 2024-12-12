Here's a **comprehensive Seaborn cheatsheet** for quick reference, covering key functionalities and customizations for creating beautiful and informative statistical plots.

---

# 📊 **Seaborn Cheatsheet**

## 1. **Setup and Import**
```python
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

# Sample dataset for examples
tips = sns.load_dataset('tips')
```

---

## 2. **Basic Seaborn Functions**

### **Set Theme and Style**
```python
sns.set_theme(style="whitegrid", palette="pastel")
```
- **Themes**: `darkgrid`, `whitegrid`, `dark`, `white`, `ticks`
- **Color Palettes**: `pastel`, `muted`, `bright`, `deep`, `dark`, `colorblind`

### **Load Built-in Datasets**
```python
df = sns.load_dataset('tips')  # Built-in dataset
print(df.head())
```

---

## 3. **Relational Plots**

### **Scatter Plot**
```python
sns.scatterplot(x='total_bill', y='tip', data=tips, hue='sex', size='size', style='time')
plt.title('Scatter Plot')
plt.show()
```
- **`hue`**: Color based on categories
- **`size`**: Marker size
- **`style`**: Different marker styles

### **Line Plot**
```python
sns.lineplot(x='size', y='total_bill', data=tips, hue='sex', style='time', markers=True)
plt.title('Line Plot')
plt.show()
```
- Use **`markers=True`** for marker symbols.

### **Relplot (Flexible Relational Plot)**
```python
sns.relplot(x='total_bill', y='tip', data=tips, kind='scatter', col='time', hue='sex')
plt.show()
```
- **`kind`**: `scatter`, `line`
- **`col`**: Create subplots for categories.

---

## 4. **Categorical Plots**

### **Strip Plot (Jittered Scatter)**
```python
sns.stripplot(x='day', y='total_bill', data=tips, jitter=True, hue='sex', palette='deep', dodge=True)
plt.title('Strip Plot')
plt.show()
```

### **Swarm Plot (Avoid Overlaps)**
```python
sns.swarmplot(x='day', y='total_bill', data=tips, hue='sex', dodge=True)
plt.title('Swarm Plot')
plt.show()
```

### **Box Plot**
```python
sns.boxplot(x='day', y='total_bill', data=tips, hue='sex', palette='coolwarm')
plt.title('Box Plot')
plt.show()
```

### **Violin Plot**
```python
sns.violinplot(x='day', y='total_bill', data=tips, hue='sex', split=True, palette='muted')
plt.title('Violin Plot')
plt.show()
```
- **`split=True`**: Splits the violin for each hue.

### **Bar Plot**
```python
sns.barplot(x='day', y='total_bill', data=tips, hue='sex', estimator=np.mean, ci='sd')
plt.title('Bar Plot')
plt.show()
```
- **`estimator`**: Aggregation function (`np.mean`, `np.sum`)
- **`ci`**: Confidence interval (`sd`, `None`)

### **Count Plot**
```python
sns.countplot(x='day', data=tips, hue='sex')
plt.title('Count Plot')
plt.show()
```

### **Point Plot**
```python
sns.pointplot(x='day', y='total_bill', data=tips, hue='sex', dodge=True, markers='o')
plt.title('Point Plot')
plt.show()
```

---

## 5. **Distribution Plots**

### **Histogram**
```python
sns.histplot(tips['total_bill'], bins=20, kde=True, color='skyblue')
plt.title('Histogram')
plt.show()
```
- **`kde=True`**: Adds a density curve.

### **KDE Plot (Density Plot)**
```python
sns.kdeplot(x='total_bill', data=tips, hue='sex', fill=True)
plt.title('KDE Plot')
plt.show()
```

### **ECDF Plot**
```python
sns.ecdfplot(x='total_bill', data=tips, hue='sex')
plt.title('ECDF Plot')
plt.show()
```

### **Joint Plot**
```python
sns.jointplot(x='total_bill', y='tip', data=tips, kind='hex', color='purple')
plt.show()
```
- **`kind`**: `scatter`, `hex`, `kde`, `hist`, `reg`

### **Pair Plot**
```python
sns.pairplot(tips, hue='sex', palette='husl')
plt.show()
```

---

## 6. **Heatmaps**

### **Correlation Heatmap**
```python
corr = tips.corr()
sns.heatmap(corr, annot=True, cmap='coolwarm', linewidths=0.5)
plt.title('Correlation Heatmap')
plt.show()
```

### **Custom Heatmap**
```python
data = np.random.rand(10, 12)
sns.heatmap(data, cmap='viridis', annot=True, fmt='.2f', linewidths=0.2)
plt.title('Heatmap Example')
plt.show()
```
- **`annot=True`**: Adds numerical values.
- **`fmt`**: String formatting for annotations.

---

## 7. **Regression Plots**

### **Regression Line with Scatter Plot**
```python
sns.regplot(x='total_bill', y='tip', data=tips, scatter_kws={'color':'blue'}, line_kws={'color':'red'})
plt.title('Regression Plot')
plt.show()
```

### **LM Plot (Multiple Regplots)**
```python
sns.lmplot(x='total_bill', y='tip', data=tips, hue='sex', col='time', height=5)
plt.show()
```
- **`col`**: Facets into multiple subplots.

---

## 8. **FacetGrid**

### **FacetGrid for Multiple Plots**
```python
g = sns.FacetGrid(tips, col="time", hue="sex", height=4, aspect=1.2)
g.map(sns.scatterplot, "total_bill", "tip").add_legend()
plt.show()
```

---

## 9. **Customizing Plots**

### **Setting Titles and Labels**
```python
sns.boxplot(x='day', y='total_bill', data=tips)
plt.title('Box Plot')
plt.xlabel('Days of the Week')
plt.ylabel('Total Bill ($)')
plt.show()
```

### **Adjusting Figure Size**
```python
plt.figure(figsize=(10, 6))
sns.barplot(x='day', y='total_bill', data=tips)
plt.show()
```

### **Changing Colors**
```python
sns.set_palette('pastel')  # Set color palette
sns.barplot(x='day', y='total_bill', data=tips)
plt.show()
```

---

## 10. **Saving Figures**
```python
plt.figure(figsize=(8, 6))
sns.boxplot(x='day', y='total_bill', data=tips)
plt.title('Saved Plot')
plt.savefig('boxplot.png', dpi=300, bbox_inches='tight')
plt.show()
```

---

## 11. **Useful Color Palettes**

### Seaborn Built-in Palettes:
```python
sns.color_palette('deep')       # Default palette
sns.color_palette('pastel')     # Light colors
sns.color_palette('muted')      # Muted tones
sns.color_palette('dark')       # Darker tones
sns.color_palette('colorblind') # Colorblind-safe
```

### Custom Palette Example:
```python
custom_palette = ['#3498db', '#e74c3c', '#2ecc71']
sns.set_palette(custom_palette)
```

---

## 12. **Tips and Tricks**
1. **Reset Settings**: Use `sns.reset_defaults()` to reset to defaults.
2. **Interactive Mode**: Use `%matplotlib inline` (Jupyter) for inline plots.
3. **Save Time**: Use `FacetGrid` or `relplot` to generate subplots efficiently.
4. **Avoid Overplotting**: Use `swarmplot` or `stripplot` with `jitter=True`.

---

This **Seaborn cheatsheet** covers the most common plots, configurations, and customization options. Seaborn is built to simplify complex visualizations while ensuring aesthetic appeal. For more advanced options, check the [official Seaborn documentation](https://seaborn.pydata.org/). 🚀