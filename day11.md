# Daily Diary – Day 11
`Date : 4/7/26`
**Subject:** Python Programming
#### **Topic Covered:** Pandas – Series, DataFrame, Indexing, Slicing, Missing Values, Grouping, Custom Functions, Joining & Reading CSV

---

## 1. What is Pandas? (Brief Theory)
**Pandas** is a powerful Python library for data manipulation and analysis. It provides two key data structures — **Series** (1D) and **DataFrame** (2D) — that make working with structured data fast and easy.

```python
import numpy as np
import pandas as pd
```

---

## 2. Series (1D Data Structure)
**Theory:** A Series is a one-dimensional labeled array. It can hold any data type (int, string, float, etc.).

```python
l1 = [1, 2, 3, 4, 5, 6]
labels = ['a', 'b', 'c', 'd', 'e', 'f']
d1 = {"A": 10, "B": 20, "C": 30, "D": 40, "E": 50}

s1 = pd.Series(l1)                   # default index (0, 1, 2...)
print(type(s1))                       # <class 'pandas.core.series.Series'>
print(s1[4])                          # access by index -> 5

s2 = pd.Series(labels)               # Series of strings
print(s2[4])                          # 'e'

s3 = pd.Series(data=l1, index=labels) # custom labels as index
print(s3['a'])                         # 1
print(s3[0])                           # 1

pd.Series(d1)                         # Series from dictionary
```

---

## 3. DataFrame (2D Data Structure)
**Theory:** A DataFrame is a 2D table with labeled rows and columns — like an Excel sheet. Each column is a Series.

```python
arr = np.random.randint(low=1, high=100, size=(5, 6))

data = pd.DataFrame(arr)                # default index and columns
print(type(data))

df = pd.DataFrame(arr,
                  index=["A", "B", "C", "D", "E"],
                  columns=["U", "V", "W", "X", "Y", "Z"])
print(df)
```

---

## 4. Grabbing Columns

```python
df["X"]              # single column → returns Series
df[["X", "Z", "V"]] # multiple columns → returns DataFrame
```

---

## 5. Grabbing Rows

```python
df.loc["C"]            # row by label
df.loc[["A", "B", "E"]]  # multiple rows by label
df.iloc[2]             # row by integer position (0-based)
```

---

## 6. Adding a New Column

```python
df['New'] = [10, 20, 30, 40, 50]    # add new column
print(df)

df['New'] = [100, 200, 300, 400, 500]  # update existing column
print(df)
```

---

## 7. Deleting a Column

```python
df.drop('New', axis=1)                  # axis=1 means column (does NOT modify original)
df.drop('New', axis=1, inplace=True)    # inplace=True modifies original DataFrame
print(df)
```

---

## 8. Conditional Selection (Filtering)

```python
df['X']                                 # column X values
df['X'] % 2 == 0                        # boolean mask
df[df['X'] % 2 == 0]                    # rows where X is even
df[df['X'] % 2 == 0]['Y']              # column Y for even X rows

# multiple conditions using & (AND), | (OR)
(df['X'] % 2 == 0) & (df['X'] > 50)
df[(df['X'] % 2 == 0) & (df['X'] > 50)]
```

---

## 9. Setting/Resetting Index

```python
df.reset_index()                        # reset index to 0,1,2... (does not modify original)
df.reset_index(inplace=True)            # modifies original

df['States'] = "PB RJ DL CHD J&K".split()  # add new column
print("PB RJ DL CHD J&K".split())           # ['PB', 'RJ', 'DL', 'CHD', 'J&K']

df.set_index('States')                  # set States column as index
```

---

## 10. Missing Values (NaN Handling)

```python
d = {"A": [1, 2, 3, np.nan],
     "B": [5, np.nan, np.nan, np.nan],
     "C": [10, 20, 30, 40],
     "D": [np.nan, np.nan, np.nan, np.nan]}

df = pd.DataFrame(d)

df.isnull()                 # shows True/False for each cell
df.isnull().sum()           # count of NaN per column
df.dropna(axis=1)           # drop columns with any NaN
df.dropna(axis=1, thresh=2) # drop columns with fewer than 2 non-NaN values
df.fillna("FILL")           # fill all NaN with "FILL"
df.fillna(df.mean())        # fill NaN with column mean
df.fillna(0)                # fill NaN with 0
```

---

## 11. Grouping (GroupBy)

```python
d = {"Company":  ["FB", "GOOGLE", "MICROSOFT", "FB", "GOOGLE", "FB", "MICROSOFT", "FB"],
     "Employee": ["Sam", "Rachel", "Maddy", "Joe", "Srishti", "Shivay", "Pushpa", "Kirti"],
     "Sales":    [1000, 500, 550, 2000, 890, 500, 350, 350]}

df = pd.DataFrame(d)

df.min()                    # min across all numeric columns
df.max()                    # max across all numeric columns

grouped_df = df.groupby('Company')   # group by Company
grouped_df.min()                      # min for each company
grouped_df.max()                      # max for each company
grouped_df.describe()                 # stats for each company
df.describe()                         # overall stats
```

---

## 12. Custom Functions (apply)

```python
def give_bonus(sales):
    return sales + 100

df['Sales'].apply(give_bonus)             # apply custom function

# lambda shorthand
df['Sales'] = df['Sales'].apply(lambda sales: sales + 100)
print(df)
```

---

## 13. Joining / Concatenating DataFrames

```python
new_employee = pd.DataFrame({'Company': ['GOOGLE'], 'Employee': ['Kriti'], 'Sales': [5000]})

df = pd.concat([df, new_employee])       # add row to df
df.index.values[-1] = 8                  # fix index

# concat with different columns (NaN fills missing)
another_employee = pd.DataFrame({'Company': ['INFOSYS'], 'Employee': ['XYZ'], 'Gender': ['M']})
pd.concat([df, another_employee])

df.drop(1)                               # drop row at index 1
df[df['Company'] == 'MICROSOFT'].index  # get index of rows matching condition
```

---

## 14. Reading a CSV File

```python
df = pd.read_csv("/content/Ecommerce Purchases.csv")

df.head(10)      # first 10 rows
df.head(15)      # first 15 rows
df.tail()        # last 5 rows (default)
df.sample(5)     # 5 random rows
df.columns       # column names
df.shape         # (rows, columns)
df.info()        # data types, non-null counts
df.describe()    # statistical summary
```

---

## 15. Quick Reference Table

| Function | Purpose |
|---|---|
| `pd.Series()` | Create 1D labeled array |
| `pd.DataFrame()` | Create 2D table |
| `df["col"]` | Select column |
| `df.loc["row"]` | Select row by label |
| `df.iloc[n]` | Select row by position |
| `df.drop()` | Drop row/column |
| `df.isnull()` | Check for NaN |
| `df.fillna()` | Fill missing values |
| `df.dropna()` | Drop rows/cols with NaN |
| `df.groupby()` | Group rows |
| `df.apply()` | Apply function to column |
| `pd.concat()` | Join DataFrames |
| `pd.read_csv()` | Load CSV file |
| `df.describe()` | Statistical summary |
| `df.info()` | Column types & counts |

---

## Summary of Day 11
Today I learned **Pandas** — the most important data analysis library in Python. I covered **Series** (1D labeled array) and **DataFrame** (2D table), practiced selecting columns and rows using `loc`, `iloc`, and bracket notation, added and deleted columns, applied conditional filters using boolean masks, handled **missing values** using `isnull`, `fillna`, and `dropna`, used **groupby** for grouped analysis, applied **custom functions** with `apply` and `lambda`, **concatenated** DataFrames, and loaded a real CSV dataset using `pd.read_csv()`.

**Practice Questions for Tomorrow:**
1. Create a Series from a dictionary of 5 students and their marks.
2. Create a 4×3 DataFrame with custom row and column labels.
3. Read any CSV file and display its shape, columns, and first 5 rows.
4. Filter rows where Sales > 500 from the company DataFrame.
5. Group the company data by Company and find the sum of sales per company.