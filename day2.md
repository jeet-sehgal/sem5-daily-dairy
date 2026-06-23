# Daily Diary – Day 2
`Date : 23/6/26`

**Subject:** Python Programming
##### **Topic Covered:** Python Operators – Arithmetic, Bitwise, Assignment, Comparison, Logical, Identity, Membership

---

## 1. Introduction to Operators (Brief Theory)
Operators are special symbols used to perform operations on variables/values. Python has **7 kinds of operators**:
1. Arithmetic
2. Bitwise
3. Assignment
4. Comparison / Relational
5. Logical
6. Identity
7. Membership

---

## 2. Arithmetic Operators
**Theory:** Used to perform basic math — addition, subtraction, multiplication, division, modulus, exponentiation, floor division.

```python
x, y = 5, 2
print(f'x + y = {x + y}')    # 7
print(f'x - y = {x - y}')    # 3
print(f'x * y = {x * y}')    # 10
print(f'x / y = {x / y}')    # 2.5
print(f'x % y = {x % y}')    # 1
print(f'x ** y = {x ** y}')  # 25
print(f'x // y = {x // y}')  # 2
```

## 3. Bitwise Operators
**Theory:** Perform operations on the bit-level representation of numbers (`&`, `|`, `^`, `~`, `<<`, `>>`).

```python
x, y = 5, 2
print(x & y)    # AND  -> 0
print(x | y)    # OR   -> 7
print(x ^ y)    # XOR  -> 7
print(~x)       # NOT  -> -6
print(x << y)   # Left shift  -> 20
print(x >> y)   # Right shift -> 1
```

## 4. Assignment Operators
**Theory:** Used to assign/update values in a variable in a shorthand way (`=`, `+=`, `-=`, `*=`, etc.).

```python
x, y = 5, 2

x += y; print(x)   # 7
x, y = 5, 2
x -= y; print(x)   # 3
x, y = 5, 2
x *= y; print(x)   # 10
x, y = 5, 2
x /= y; print(x)   # 2.5
x, y = 5, 2
x %= y; print(x)   # 1
x, y = 5, 2
x **= y; print(x)  # 25
x, y = 5, 2
x //= y; print(x)  # 2
x, y = 5, 2
x &= y; print(x)   # 0
x, y = 5, 2
x |= y; print(x)   # 7
x, y = 5, 2
x ^= y; print(x)   # 7
x, y = 5, 2
x <<= y; print(x)  # 20
x, y = 5, 2
x >>= y; print(x)  # 1
```

## 5. Comparison (Relational) Operators
**Theory:** Used to compare two operands; result is always `True`/`False` (`==`, `!=`, `>`, `<`, `>=`, `<=`).

```python
x, y = 5, 2
print(x == y)   # False
print(x != y)   # True
print(x > y)    # True
print(x < y)    # False
print(x >= y)   # True
print(x <= y)   # False
```

## 6. Logical Operators
**Theory:** Combine multiple conditions (`and`, `or`, `not`).

```python
x, y = True, False
print(x and y)   # False
print(x or y)    # True
print(not x)     # False
```

## 7. Identity Operators
**Theory:** `is` and `is not` check whether two variables point to the **same object** in memory (compare using `id()`), not just equal values.

```python
# Same reference
x = [1, 2, 3]
y = x
print(x is y)       # True
print(x is not y)   # False
print(id(x), id(y)) # same id

# Different reference, same values
x = [1, 2, 3]
y = [1, 2, 3]
print(x is y)       # False
print(x is not y)   # True
print(id(x), id(y)) # different ids
```

## 8. Membership Operators
**Theory:** `in` and `not in` check whether an element exists inside a sequence (list, string, tuple, etc.).

```python
x = 1
y = [1, 2, 3]
print(x in y)        # True

x = 8
y = [1, 2, 3]
print(x not in y)    # True
```

---

## 9. Practice Program – Combining All Operators
```python
a, b = 10, 3

# Arithmetic
print("Sum:", a + b)
print("Power:", a ** b)

# Comparison
print("Is a greater than b?", a > b)

# Logical
print("a>5 and b<5:", a > 5 and b < 5)

# Assignment
a += b
print("After a += b:", a)

# Membership
nums = [10, 20, 30]
print("Is 20 in nums?", 20 in nums)

# Identity
c = nums
print("c is nums?", c is nums)
```

---

## Summary of Day 2
Today I learned about all **7 types of operators in Python** — Arithmetic, Bitwise, Assignment, Comparison, Logical, Identity, and Membership. I practiced each one with short code snippets, understood the difference between `==` (value equality) and `is` (reference/identity equality), and saw how shorthand assignment operators (`+=`, `-=`, etc.) simplify code.

