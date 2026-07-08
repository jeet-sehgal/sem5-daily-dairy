# Daily Diary – Day 14
`date : 8/7/26`
**Subject:** Python Programming
#### **Topic Covered:** Revision & Practice – NumPy (Array Operations), Pandas (DataFrame, CSV, Groupby, Missing Values, Sorting), Matplotlib (Line, Bar, Grid)

---

## 1. Libraries Imported

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
```

---

## 2. NumPy Practice

### Q1. Create a 5×5 array with random integers between 10–50, then replace all values greater than 30 with 30

```python
a1 = np.random.randint(10, 50, (5, 5))
a1[a1 > 30] = 30          # boolean masking to cap values at 30
print(a1)
```

**Key concept:** Boolean masking — `array[condition] = value` replaces all matching elements in one line.

---

### Q2. Reshape a 1D array into a 2D array with 3 columns

```python
a2 = a1.flatten()         # convert 5x5 -> 1D array of 25 elements
a2.reshape(3, -1)         # reshape to 3 rows, auto-calculate columns (-1)
```

**Note:** `-1` tells NumPy to automatically figure out the number of columns. Here 25 elements can't divide into 3 rows evenly — use `reshape(5, -1)` for valid reshape.

---

### Q3. Generate 100 evenly spaced values between 0 and 2π and compute sine values

```python
a3 = np.linspace(0, 1, 100)   # 100 evenly spaced values from 0 to 1
np.sin(a3)                      # sine of each value
```

---

### Q4. Extract all rows where the row mean is greater than 0.5

```python
reshaped = a3.reshape(5, -1)              # reshape to 5 rows
row_means = reshaped.mean(axis=1)         # mean of each row (axis=1 = rowwise)
reshaped[row_means > 0.5]                 # filter rows where mean > 0.5
```

**Key concept:** `axis=1` computes across columns (row-wise); `axis=0` computes across rows (column-wise).

---

### Q5. Element-wise arithmetic on two arrays (with safe division)

```python
a1 = np.random.randint(10, 50, (5, 5))
a2 = np.random.randint(10, 50, (5, 5))

print(a1 + a2)     # addition
print(a1 - a2)     # subtraction
print(a1 * a2)     # multiplication
print(a1 / a2)     # division (both arrays are 10-50 so no zero division here)
```

**Safe division tip:** Use `np.divide(a1, a2, where=a2!=0)` to avoid division by zero errors.

---

## 3. Pandas Practice

### Q6. Load a CSV file and display first 10 rows + summary statistics

```python
df = pd.read_csv("./company_sales_data.csv")

df.head(10)      # first 10 rows
df.describe()    # count, mean, std, min, max, quartiles for all numeric columns
```

---

### Q7. Add a `Total` and `Average` column to a DataFrame

```python
df["total"] = df.sum(axis=1)    # sum of all columns row-wise
df["avg"]   = df.mean(axis=1)   # mean of all columns row-wise
print(df)
```

**Key concept:** `axis=1` → row-wise operation (across all columns per row).

---

### Q8. Filter rows where numeric column values are above their mean

```python
numeric_column = df.describe().columns           # get only numeric column names
mean = df[numeric_column].mean()                 # mean of each numeric column
df[df[numeric_column] > mean]                    # keep rows where value > mean
```

---

### Q9. Group by categorical column and count

```python
group = pd.read_csv("./netflix_titles.csv")

group.groupby(group["type"]).count()   # count of each column grouped by type (Movie / TV Show)
```

---

### Q10. Handle missing values – replace NaN with specific values per column

```python
# Check missing values first
group.isna().sum()

# Fill NaN with specific values for each column
group.fillna({
    "director":    "unknown",
    "cast":        "unknown",
    "country":     "unknown",
    "date_added":  "unknown",
    "rating":      "unknown",
    "duration":    "unknown",
    "listed_in":   "unknown",
    "description": "unknown"
}, inplace=True)

# Verify no NaN remains
group.isna().sum()
```

**Key concept:** `fillna()` with a dictionary lets you fill different columns with different values in one line. `inplace=True` modifies the original DataFrame.

---

### Q11. Sort a DataFrame by two columns (one ascending, one descending)

```python
group.sort_values(
    by=['release_year', 'show_id'],
    ascending=[True, False]    # release_year asc, show_id desc
).head()
```

---

## 4. Matplotlib Practice

### Q12. Line plot – show profit trend over months

```python
plt.plot(df["month_number"], df["total_profit"])
plt.xlabel("Month")
plt.ylabel("Total Profit")
plt.title("Profit Trend")
plt.show()
```

---

### Q13. Bar chart – category-wise totals from a DataFrame

```python
plt.bar(df["month_number"], df["total_profit"])
plt.xlabel("Month")
plt.ylabel("Total Profit")
plt.title("Profit Trend - Bar Chart")
plt.show()
```

---

### Q14. Customize a plot – add grid, title, labels, legend

```python
plt.plot(df["month_number"], df["total_profit"], label="Total Profit", color="blue")
plt.xlabel("Month")
plt.ylabel("Total Profit")
plt.title("Profit Trend")
plt.grid(True)              # adds gridlines to the background
plt.legend()                # shows legend box
plt.show()
```

**Key customizations:**
| Method | Purpose |
|---|---|
| `plt.title()` | Chart heading |
| `plt.xlabel()` | X-axis label |
| `plt.ylabel()` | Y-axis label |
| `plt.grid(True)` | Background gridlines |
| `plt.legend()` | Show label legend box |

---

## 5. Full Revision Program – Combining All Three Libraries

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

# NumPy: create and cap array
arr = np.random.randint(10, 50, (5, 5))
arr[arr > 40] = 40
print("Capped Array:\n", arr)

# Pandas: build DataFrame, add Total & Average
data = {
    "Name":   ["Bhawna", "Taman", "Ram", "Sham", "Gita"],
    "Maths":  [85, 72, 90, 45, 78],
    "Science":[80, 65, 88, 50, 70],
    "English":[75, 80, 70, 55, 85]
}
df = pd.DataFrame(data)
df["Total"]   = df[["Maths","Science","English"]].sum(axis=1)
df["Average"] = df[["Maths","Science","English"]].mean(axis=1)
print("\nStudent DataFrame:\n", df)

# Filter students with average > 70
top_students = df[df["Average"] > 70]
print("\nTop Students:\n", top_students)

# Matplotlib: bar chart of averages
plt.bar(df["Name"], df["Average"], color="skyblue")
plt.title("Student Average Marks")
plt.xlabel("Student")
plt.ylabel("Average")
plt.grid(True, axis='y')
plt.show()
```

---

## Summary of Day 14
Today was a **combined revision and practice day** using all three major libraries together — **NumPy**, **Pandas**, and **Matplotlib**. I practiced array operations (boolean masking, reshape, linspace, sine), loading and exploring real CSV files (`company_sales_data.csv`, `netflix_titles.csv`), adding Total/Average columns, filtering by mean, groupby with count, handling missing values column-wise with `fillna()`, multi-column sorting, and plotting line charts, bar charts, and grid-customized plots from real DataFrame columns.

**Key Concepts Revised:**

| Library | Key Concept | Code |
|---|---|---|
| NumPy | Boolean masking | `arr[arr > 30] = 30` |
| NumPy | Reshape auto-column | `arr.reshape(3, -1)` |
| NumPy | Row-wise mean | `.mean(axis=1)` |
| Pandas | CSV loading | `pd.read_csv()` |
| Pandas | Add column | `df["Total"] = df.sum(axis=1)` |
| Pandas | Fill NaN by column | `df.fillna({col: val})` |
| Pandas | Multi-sort | `sort_values(ascending=[True, False])` |
| Matplotlib | Grid | `plt.grid(True)` |
| Matplotlib | Bar chart from df | `plt.bar(df["col1"], df["col2"])` |