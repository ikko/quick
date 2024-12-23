Here's a comprehensive **Matplotlib `pyplot`** cheatsheet for quick reference. It covers common functions, parameters, and essential tips for creating and customizing visualizations.

---

# 📊 **Matplotlib Pyplot Cheatsheet**

## 1. **Setup and Import**
```python
import matplotlib.pyplot as plt
import numpy as np
```

---

## 2. **Basic Plotting**

### **Line Plot**
```python
x = np.linspace(0, 10, 100)  # Generate 100 evenly spaced points
y = np.sin(x)                # Example data

plt.plot(x, y, label='sin(x)', color='blue', linestyle='-', linewidth=2, marker='o')
plt.title('Line Plot')
plt.xlabel('X-axis')
plt.ylabel('Y-axis')
plt.legend()
plt.grid(True)
plt.show()
```

### Key Arguments:
- **`color`**: Line color (`'blue'`, `'r'`, `'#ff1234'`)
- **`linestyle`**: `'solid'` (`'-'`), `'dashed'` (`'--'`), `'dashdot'` (`'-.`'), `'dotted'` (`':'`)
- **`linewidth`**: Line thickness
- **`marker`**: Markers (`'o'`, `'x'`, `'*'`, `'s'`, `'.'`)
- **`label`**: Adds label for legend

---

## 3. **Multiple Plots**

### **Overlay Multiple Lines**
```python
x = np.linspace(0, 10, 100)
plt.plot(x, np.sin(x), label='sin(x)')
plt.plot(x, np.cos(x), label='cos(x)')
plt.legend()
plt.show()
```

### **Subplots**
```python
fig, ax = plt.subplots(2, 2, figsize=(8, 6))  # 2x2 grid of subplots
ax[0, 0].plot(x, np.sin(x))
ax[0, 1].plot(x, np.cos(x))
ax[1, 0].plot(x, x**2)
ax[1, 1].plot(x, -x**2)

plt.tight_layout()
plt.show()
```

- **`figsize`**: Figure size `(width, height)`
- **`tight_layout()`**: Prevents overlapping

---

## 4. **Scatter Plot**
```python
x = np.random.rand(50)
y = np.random.rand(50)
colors = np.random.rand(50)
sizes = 500 * np.random.rand(50)

plt.scatter(x, y, c=colors, s=sizes, alpha=0.5, edgecolor='black')
plt.title('Scatter Plot')
plt.xlabel('X')
plt.ylabel('Y')
plt.colorbar(label='Color Scale')
plt.show()
```

### Key Arguments:
- **`c`**: Colors
- **`s`**: Marker size
- **`alpha`**: Transparency
- **`edgecolor`**: Edge color for markers

---

## 5. **Bar Plots**

### **Vertical Bar Plot**
```python
categories = ['A', 'B', 'C', 'D']
values = [3, 7, 5, 2]

plt.bar(categories, values, color='skyblue', edgecolor='black')
plt.title('Bar Plot')
plt.xlabel('Categories')
plt.ylabel('Values')
plt.show()
```

### **Horizontal Bar Plot**
```python
plt.barh(categories, values, color='lightgreen', edgecolor='black')
plt.title('Horizontal Bar Plot')
plt.show()
```

---

## 6. **Histogram**
```python
data = np.random.randn(1000)  # Normally distributed data

plt.hist(data, bins=30, color='purple', edgecolor='black', alpha=0.7)
plt.title('Histogram')
plt.xlabel('Value')
plt.ylabel('Frequency')
plt.grid(axis='y')
plt.show()
```

### Key Arguments:
- **`bins`**: Number of bins
- **`alpha`**: Transparency
- **`edgecolor`**: Bin edge color

---

## 7. **Pie Chart**
```python
sizes = [15, 30, 45, 10]
labels = ['A', 'B', 'C', 'D']
colors = ['gold', 'lightblue', 'lightgreen', 'red']
explode = (0, 0.1, 0, 0)  # Explode slice B

plt.pie(sizes, labels=labels, colors=colors, explode=explode, autopct='%1.1f%%', shadow=True)
plt.title('Pie Chart')
plt.show()
```

---

## 8. **Customizing Axes and Ticks**

### **Logarithmic Scale**
```python
plt.plot(x, x**2)
plt.yscale('log')  # Logarithmic scale for Y-axis
plt.title('Log Scale')
plt.show()
```

### **Setting Ticks**
```python
plt.plot(x, np.sin(x))
plt.xticks(np.arange(0, 11, 1))  # Custom X ticks
plt.yticks([-1, 0, 1], ['Low', 'Medium', 'High'])
plt.show()
```

### **Axes Limits**
```python
plt.plot(x, np.sin(x))
plt.xlim(0, 5)  # X-axis range
plt.ylim(-1, 1)  # Y-axis range
plt.show()
```

---

## 9. **Adding Annotations**
```python
plt.plot(x, np.sin(x))
plt.annotate('Maximum', xy=(1.5*np.pi, 1), xytext=(4, 1.5),
             arrowprops=dict(facecolor='black', arrowstyle='->'))
plt.title('Annotation Example')
plt.show()
```

---

## 10. **Saving Figures**
```python
plt.plot(x, np.sin(x))
plt.title('Save Example')
plt.savefig('plot.png', dpi=300, bbox_inches='tight')
plt.show()
```
- **`dpi`**: Image resolution
- **`bbox_inches='tight'`**: Removes extra whitespace

---

## 11. **Figure and Axis Objects**

### Creating Figures with `Figure` and `Axes`
```python
fig, ax = plt.subplots(figsize=(6, 4))

ax.plot(x, np.sin(x), label='sin(x)')
ax.set_title('Figure and Axes Example')
ax.set_xlabel('X-axis')
ax.set_ylabel('Y-axis')
ax.legend()

plt.show()
```

### Adding Multiple Axes to a Figure
```python
fig = plt.figure()
ax1 = fig.add_axes([0.1, 0.1, 0.8, 0.8])  # Main axes
ax2 = fig.add_axes([0.5, 0.5, 0.3, 0.3])  # Inset axes

ax1.plot(x, np.sin(x))
ax2.plot(x, np.cos(x), color='red')
plt.show()
```

---

## 12. **Heatmap (Using `imshow`)**
```python
data = np.random.rand(10, 10)  # 10x10 matrix

plt.imshow(data, cmap='viridis', interpolation='nearest')
plt.colorbar(label='Color Scale')
plt.title('Heatmap Example')
plt.show()
```

### Key Arguments:
- **`cmap`**: Colormap (`'viridis'`, `'plasma'`, `'gray'`)
- **`interpolation`**: Controls pixel smoothing

---

## 13. **Common Colormaps**
| Sequential | Diverging  | Cyclic   |
|------------|------------|----------|
| `viridis`  | `coolwarm` | `twilight` |
| `plasma`   | `seismic`  | `hsv`      |
| `magma`    | `Spectral` | `twilight_shifted` |

---

## 14. **Tips and Tricks**
1. **Grid**: Use `plt.grid(True)` to add a grid.
2. **Multiple Figures**: Use `plt.figure()` to create multiple figures.
3. **Show Multiple Plots**: Use `plt.show()` only once after all plots.
4. **Interactive Mode**: Use `plt.ion()` for live updating plots.

---

This cheatsheet provides a solid reference for most **`matplotlib.pyplot`** use cases. For more details, check the official [Matplotlib Documentation](https://matplotlib.org/stable/contents.html). 🚀