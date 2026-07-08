# Daily Diary – Day 13
`Date : 7/7/26`
**Subject:** Python Programming
#### **Topic Covered:** Matplotlib – Line Plot, Markers, Linestyle, Colors, Labels, Subplots, Figure, Pie Chart, Bar Graph, Histogram, Box Plot

---

## 1. What is Matplotlib? (Brief Theory)
**Matplotlib** is a Python library used for creating visualizations like graphs, charts, and plots. It helps represent data in a clear and easy-to-understand way, making it useful for data analysis and presentations.

```python
import matplotlib.pyplot as plt
import numpy as np
```

---

## 2. Basic Line Plot

```python
# Simple line from two points
xaxis = np.array([1, 3])
yaxis = np.array([0, 2])
plt.plot(xaxis, yaxis)
plt.show()

# Another simple line
x = np.array([1, 2])
y = np.array([2, 3])
plt.plot(x, y)
plt.show()

# Plotting with only y values (x auto-assigned as 0,1,2...)
x = np.array([2, 4, 5, 7, 8, 9, 9])
plt.plot(x)
plt.show()
```

### Plotting from a CSV file
```python
import pandas as pd

x = pd.read_csv('/content/Salaries.csv')
plt.plot(x['TotalPayBenefits'])
plt.show()
```

---

## 3. Markers
**Theory:** Markers emphasize each data point on the plot using special symbols.

```python
# Star marker (*)
x = np.array([1, 2])
y = np.array([2, 4])
plt.plot(x, y, marker='*')
plt.show()

# Plus marker (+)
a = np.array([3, 0])
b = np.array([0, 2])
plt.plot(a, b, marker='+')
plt.show()
```

---

## 4. Linestyle
**Theory:** Controls how the line looks — `dotted`, `dashed`, `dashdot`, `solid` (default).

```python
# Dashdot line with + marker
a = np.array([3, 1])
b = np.array([1, 2])
plt.plot(a, b, marker='+', linestyle='dashdot')
plt.show()

# Dotted line with * marker
k = np.array([5, 2])
r = np.array([2, 5])
plt.plot(k, r, marker='*', linestyle='dotted')
plt.show()

# Multiple points with dotted line
r = np.array([2, 5, 6, 8, 3])
plt.plot(r, marker='*', linestyle='dotted')
plt.show()
```

---

## 5. Color, Line Width & Marker Styling

**Theory:** Key styling parameters:
| Parameter | Use |
|---|---|
| `color` | Line color (`'r'`, `'g'`, `'b'`, `'darkred'`) |
| `linewidth` | Thickness of the line |
| `ms` | Marker size |
| `mec` | Marker edge color |
| `mfc` | Marker face color |

```python
# Color of line
a = np.array([3, 1, 5, 8, 2])
plt.plot(a, marker='+', linestyle='dashdot', color='g')
plt.show()

# Full styling - linewidth, marker size, marker colors
xaxis = np.array([1, 3, 4, 5])
yaxis = np.array([0, 2, 2, 6])
plt.plot(xaxis, yaxis, marker='*', color='b', ms='20', mec='r', mfc='g', linewidth='3')
plt.show()

# Two lines on same plot
x = np.array([5, 7, 3, 2, 8, 9])
y = np.array([1, 2, 3, 4, 5, 9])
plt.plot(x, marker='+', ms='30', mec='g')
plt.plot(y)
plt.show()
```

---

## 6. Title & Labels with Font Styling

**Theory:** Use `font1`/`font2` dictionaries to control font family, color, and size for titles and axis labels.

```python
x = np.array([80, 85, 90, 95, 100, 105, 110, 115])
y = np.array([240, 250, 260, 270, 280, 290, 300, 77])

font1 = {'family': 'serif', 'color': 'blue',    'size': 20}
font2 = {'family': 'serif', 'color': 'darkred', 'size': 15}

plt.title("Sports Watch Data",  fontdict=font1)
plt.xlabel("Average Pulse",     fontdict=font2)
plt.ylabel("Calorie Burnage",   fontdict=font2)

plt.plot(x, y)
plt.show()
```

---

## 7. Subplots
**Theory:** `plt.subplot(rows, cols, position)` divides the figure into a grid and places plots at a given position.

```python
x = np.array([5, 7, 3, 2, 8, 9])
y = np.array([1, 2, 3, 4, 5, 9])

# 1 row, 2 columns
plt.subplot(1, 2, 1)
plt.plot(x, y)

x = np.array([5, 7, 3, 2, 3])
y = np.array([1, 2, 3, 4, 7])

plt.subplot(1, 2, 2)
plt.plot(y, x)
plt.show()

# 1 row, 4 columns
plt.subplot(1, 4, 1); plt.plot(np.array([5,7,3,2,8,9]), np.array([1,2,3,4,5,9]))
plt.subplot(1, 4, 2); plt.plot(np.array([5,7,3,2,3]),   np.array([1,2,3,4,7]))
plt.subplot(1, 4, 3); plt.plot(np.array([1,2,3,2,3]),   np.array([8,7,6,4,7]))
plt.subplot(1, 4, 4); plt.plot(np.array([1,3,5,7,8]),   np.array([2,4,6,8,0]))
plt.show()

# 2 rows, 2 columns
plt.subplot(2, 2, 1); plt.plot(np.array([5,7,3,2,8,9]), np.array([1,2,3,4,5,9]))
plt.subplot(2, 2, 2); plt.plot(np.array([5,7,3,2,3]),   np.array([1,2,3,4,7]))
plt.subplot(2, 2, 3); plt.plot(np.array([1,2,3,2,3]),   np.array([8,7,6,4,7]))
plt.subplot(2, 2, 4); plt.plot(np.array([1,3,5,7,8]),   np.array([2,4,6,8,0]))
plt.show()
```

---

## 8. Figure & Axes (Nested Plots)
**Theory:** `plt.figure()` creates a figure object. `fig.add_axes([left, bottom, width, height])` places axes manually (values between 0 and 1).

```python
x = np.array([1, 3, 5, 7, 8])
y = np.array([2, 4, 6, 8, 0])

fig = plt.figure()

# Main large plot
axes1 = fig.add_axes([0.1, 0.2, 0.9, 0.9])   # left, bottom, width, height
axes1.plot(x, y, 'r', label="red")

# Small inset plot
axes2 = fig.add_axes([0.15, 0.75, 0.3, 0.3])
axes2.plot(x, y, 'b', label="blue")

axes1.legend(loc=4)
axes2.legend()
plt.show()
```

---

## 9. Pie Chart
**Theory:** Used to show proportions of a whole. `explode` pulls out a slice. `autopct` shows percentage on the chart.

```python
# Pie chart without percentages
sizes  = [234, 567, 223, 123, 45, 239]
labels = ['Python', 'C++', 'Java', 'PHP', 'Machine Learning', 'Excel']
explode = [0.0, 0.0, 0.0, 0.2, 0.0, 0.0]   # PHP slice pulled out

plt.pie(sizes, labels=labels, explode=explode)
plt.show()

# Pie chart WITH percentage labels (autopct)
sizes   = [123, 345, 567, 889]
labels  = ['Suit', 'Jeans', 'Tops', 'Kurta']
explode = [0.0,  0.0,   0.1,   0.0]         # Tops slice pulled out

plt.pie(sizes, labels=labels, explode=explode, autopct='%1.2f%%')
plt.show()
```

---

## 10. Bar Graph
**Theory:** Vertical bars for comparing categories. Use `barh()` for horizontal bars.

```python
# Vertical bar graph (two sets)
x  = [1, 3, 4, 5, 6];  y  = [2, 4, 6, 7, 8]
x2 = [66, 33, 44];     y2 = [30, 55, 77]

plt.bar(x,  y)
plt.bar(x2, y2)
plt.title("Bar Graph")
plt.xlabel('X axis')
plt.ylabel('Y axis')
plt.show()

# Horizontal bar graph
plt.barh(x,  y)
plt.barh(x2, y2)
plt.title("Horizontal Bar Graph")
plt.xlabel('X axis')
plt.ylabel('Y axis')
plt.show()
```

---

## 11. Histogram
**Theory:** Shows the **frequency/distribution** of data. Bars represent how often values fall in a range (bin).

```python
a = np.array([33, 55, 66, 23, 45, 67, 87])
plt.hist(a)
plt.title("Histogram")
plt.show()
```

---

## 12. Box Plot
**Theory:** Shows the **spread and distribution** of data — median, quartiles, and outliers. Uses `np.random.normal(mean, std, size)` to generate data.

```python
# Generate 6 datasets with increasing standard deviation
data = [np.random.normal(0, std, 99) for std in range(1, 7)]

plt.boxplot(data)
plt.show()
```

---

## 13. Quick Reference Table

| Plot Type | Function | Use Case |
|---|---|---|
| Line Plot | `plt.plot()` | Trends over time |
| Pie Chart | `plt.pie()` | Proportions/percentages |
| Bar Chart | `plt.bar()` | Category comparison |
| Horizontal Bar | `plt.barh()` | Same but horizontal |
| Histogram | `plt.hist()` | Data distribution |
| Box Plot | `plt.boxplot()` | Spread & outliers |
| Subplot | `plt.subplot()` | Multiple plots in grid |
| Figure/Axes | `plt.figure()` | Custom positioned plots |

---

## Summary of Day 13
Today I learned **Matplotlib** — Python's core data visualization library. I practiced **line plots** with custom markers (`*`, `+`), linestyles (`dotted`, `dashdot`), colors, and line width, added **titles and axis labels** with custom font styling, used **subplots** to display multiple plots in 1×2, 1×4, and 2×2 grids, created **nested plots** using `figure()` and `add_axes()`, drew **pie charts** with explode and autopct, made **bar graphs** (vertical and horizontal), plotted **histograms** for frequency distribution, and created **box plots** to understand data spread using random normal data.

**Practice Questions for Tomorrow:**
1. Plot a sine wave using `np.sin()` with a proper title and axis labels.
2. Create a pie chart showing 5 programming languages and their popularity.
3. Draw a bar chart comparing marks of 5 students.
4. Plot two subplots side by side — one line plot and one bar chart.
5. Create a histogram of 100 random numbers generated with `np.random.randn()`.