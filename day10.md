# Daily Diary – Day 10
`Date : 3/7/26`
**Subject:** Python Programming
#### **Topic Covered:** NumPy – Arrays, Operations, Slicing, Math Functions & Practice Questions

---

## 1. What is NumPy? (Brief Theory)
**NumPy** (Numerical Python) is a powerful library for numerical computations. It provides a fast, efficient **N-dimensional array** object (`ndarray`) and mathematical functions to operate on them.

**Why NumPy over Python lists?**
| Feature | Python List | NumPy Array |
|---|---|---|
| Speed | Slower | Much faster |
| Memory | More | Less |
| Math operations | Not built-in | Built-in element-wise |
| Data type | Mixed | Same type (homogeneous) |

```python
import numpy as np
```

---

## 2. Creating Arrays

```python
import numpy as np

# 1D array
a = np.array([1, 2, 3, 4, 5])
print(a)
print(type(a))           # <class 'numpy.ndarray'>

# 2D array
b = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
print(b)

# Array properties
print(a.shape)           # (5,)
print(b.shape)           # (3, 3)
print(b.ndim)            # 2 (dimensions)
print(b.size)            # 9 (total elements)
print(b.dtype)           # int64
```

## 3. Array Creation Functions

```python
import numpy as np

# zeros, ones, full
print(np.zeros((3, 3)))           # 3x3 filled with 0.0
print(np.ones((2, 4)))            # 2x4 filled with 1.0
print(np.full((3, 3), 7))         # 3x3 filled with 7

# arange (like range)
print(np.arange(1, 21))           # 1 to 20
print(np.arange(10, 31, 2))       # even numbers 10 to 30

# linspace (evenly spaced)
print(np.linspace(0, 1, 5))       # [0, 0.25, 0.5, 0.75, 1.0]

# identity matrix
print(np.eye(4))                  # 4x4 identity matrix
```

---

## 4. Reshaping Arrays

```python
import numpy as np

a = np.arange(1, 13)              # [1, 2, 3, ..., 12]
print(a)

b = a.reshape(3, 4)               # reshape into 3x4 matrix
print(b)

c = a.reshape(4, 3)               # reshape into 4x3 matrix
print(c)

d = b.flatten()                   # back to 1D
print(d)
```

---

## 5. Indexing & Slicing

```python
import numpy as np

a = np.array([10, 20, 30, 40, 50])
print(a[0])       # 10
print(a[-1])      # 50
print(a[1:4])     # [20, 30, 40]
print(a[::2])     # [10, 30, 50]

# 2D slicing
b = np.array([[1,  2,  3,  4],
              [5,  6,  7,  8],
              [9, 10, 11, 12]])

print(b[0])         # first row  -> [1, 2, 3, 4]
print(b[1])         # second row -> [5, 6, 7, 8]
print(b[:, 2])      # third column -> [3, 7, 11]
print(b[0:2, 1:3])  # sub-matrix -> [[2,3],[6,7]]
```

---

## 6. Mathematical Operations

```python
import numpy as np

a = np.array([1, 2, 3, 4, 5])
b = np.array([10, 20, 30, 40, 50])

# Element-wise operations
print(a + b)        # [11, 22, 33, 44, 55]
print(b - a)        # [9, 18, 27, 36, 45]
print(a * b)        # [10, 40, 90, 160, 250]
print(b / a)        # [10., 10., 10., 10., 10.]
print(a ** 2)       # [1, 4, 9, 16, 25]

# Scalar operations
print(a + 100)      # [101, 102, 103, 104, 105]
print(a * 3)        # [3, 6, 9, 12, 15]
```

## 7. Statistical Functions

```python
import numpy as np

a = np.array([12, 45, 7, 23, 56, 3, 89, 34])

print("Max:", np.max(a))
print("Min:", np.min(a))
print("Sum:", np.sum(a))
print("Mean:", np.mean(a))
print("Median:", np.median(a))
print("Std Dev:", np.std(a))
print("Variance:", np.var(a))
print("Square Root:", np.sqrt(a))
print("Sorted:", np.sort(a))
```

---

## 8. Random Module in NumPy

```python
import numpy as np

# 5 random integers between 1 and 100
print(np.random.randint(1, 101, 5))

# random float values
print(np.random.rand(3))           # [0.x, 0.x, 0.x]
print(np.random.rand(2, 3))        # 2x3 float matrix

# set seed for reproducibility
np.random.seed(42)
print(np.random.randint(1, 50, 5))
```

---

## 9. Practice Questions – Solved

**Q1. Create a NumPy array of numbers from 1 to 20**
```python
arr = np.arange(1, 21)
print(arr)
# [ 1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20]
```

**Q2. Generate a 3×3 array filled with zeros**
```python
zeros = np.zeros((3, 3))
print(zeros)
```

**Q3. Create a 5×5 matrix with values 1–25 and extract diagonal elements**
```python
matrix = np.arange(1, 26).reshape(5, 5)
print(matrix)
diag = np.diag(matrix)
print("Diagonal:", diag)    # [ 1  7 13 19 25]
```

**Q4. Create a 1D array of even numbers between 10 and 30**
```python
evens = np.arange(10, 31, 2)
print(evens)    # [10 12 14 16 18 20 22 24 26 28 30]
```

**Q5. Reshape an array of 12 elements into a 3×4 matrix**
```python
arr = np.arange(1, 13)
matrix = arr.reshape(3, 4)
print(matrix)
```

**Q6. Find maximum, minimum, and mean of a NumPy array**
```python
arr = np.array([45, 12, 78, 34, 90, 23, 56])
print("Max:", np.max(arr))
print("Min:", np.min(arr))
print("Mean:", np.mean(arr))
```

**Q7. Element-wise addition, subtraction, multiplication of two arrays**
```python
a = np.array([1, 2, 3, 4, 5])
b = np.array([10, 20, 30, 40, 50])
print("Addition:", a + b)
print("Subtraction:", b - a)
print("Multiplication:", a * b)
```

**Q8. Create a 2D array and extract the second row using slicing**
```python
arr2d = np.array([[10, 20, 30],
                  [40, 50, 60],
                  [70, 80, 90]])
print("Second row:", arr2d[1])      # [40 50 60]
print("Second row (slice):", arr2d[1, :])
```

**Q9. Generate an identity matrix of size 4×4**
```python
identity = np.eye(4)
print(identity)
```

**Q10. Generate 5 random integers between 1 and 100**
```python
rand_nums = np.random.randint(1, 101, 5)
print(rand_nums)
```

**Q11. Find square root and standard deviation of elements in an array**
```python
arr = np.array([4, 9, 16, 25, 36, 49, 64])
print("Square Root:", np.sqrt(arr))
print("Std Deviation:", np.std(arr))
```

---

## 10. Useful NumPy Quick Reference

| Function | Purpose |
|---|---|
| `np.array()` | Create array |
| `np.arange()` | Range-based array |
| `np.zeros()` | Array of zeros |
| `np.ones()` | Array of ones |
| `np.eye()` | Identity matrix |
| `np.reshape()` | Change shape |
| `np.diag()` | Extract diagonal |
| `np.max/min/mean()` | Stats |
| `np.sqrt()` | Square root |
| `np.std()` | Standard deviation |
| `np.random.randint()` | Random integers |
| `np.sort()` | Sort array |

---

## Summary of Day 10
Today I learned **NumPy** — Python's most powerful library for numerical data. I practiced creating arrays using `np.array()`, `np.arange()`, `np.zeros()`, `np.ones()`, and `np.eye()`, reshaping using `.reshape()`, slicing 1D and 2D arrays, performing element-wise math operations, using statistical functions like `max`, `min`, `mean`, `std`, and `sqrt`, and generating random numbers. All 11 practice questions were solved.

**Practice Questions for Tomorrow:**
1. Create a 4×4 matrix and replace all values greater than 10 with 0.
2. Stack two 1D arrays vertically and horizontally using NumPy.
3. Find the dot product of two matrices using NumPy.
4. Normalize a NumPy array to values between 0 and 1.
5. Create a 3×3 matrix and find its transpose and determinant.