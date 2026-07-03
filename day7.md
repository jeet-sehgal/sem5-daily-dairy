# Daily Diary – Day 7
`date : 30/6/26`
**Subject:** Python Programming
#### **Topic Covered:** Function Arguments (*args, **kwargs, Positional, Keyword, Default) & Recursion

---

## 1. Types of Function Arguments (Brief Theory)
Python functions support **5 types of arguments**:
1. Positional Arguments
2. Keyword Arguments
3. Default Arguments
4. `*args` (variable positional)
5. `**kwargs` (variable keyword)

---

## 2. Positional Arguments
**Theory:** Arguments passed in the same order as the function parameters. Position matters.

```python
def student_info(name, age, city):
    print(f"Name: {name}, Age: {age}, City: {city}")

student_info("Bhawna", 21, "Ludhiana")   # correct order
# student_info(21, "Ludhiana", "Bhawna") -> wrong output, no error
```

---

## 3. Keyword Arguments
**Theory:** Arguments passed using the parameter name, so order does not matter.

```python
def student_info(name, age, city):
    print(f"Name: {name}, Age: {age}, City: {city}")

student_info(age=21, city="Ludhiana", name="Bhawna")   # order doesn't matter
student_info(name="Taman", city="Delhi", age=22)
```

---

## 4. Default Arguments
**Theory:** A default value is assigned to a parameter. If the caller doesn't pass a value, the default is used.

```python
def greet(name, message="Good Morning"):
    print(f"{message}, {name}!")

greet("Bhawna")                  # Good Morning, Bhawna!
greet("Taman", "Good Evening")   # Good Evening, Taman!

def power(base, exp=2):
    return base ** exp

print(power(5))         # 25
print(power(5, 3))      # 125
```

---

## 5. `*args` – Variable Positional Arguments
**Theory:** `*args` allows a function to accept **any number of positional arguments**. Inside the function, they are stored as a **tuple**.

```python
def total_marks(*marks):
    print(type(marks))         # <class 'tuple'>
    return sum(marks)

print(total_marks(80, 90, 70))         # 240
print(total_marks(55, 60, 75, 80, 90)) # 360

def display_names(*names):
    for name in names:
        print(f"Hello, {name}!")

display_names("Ram", "Sham", "Gita", "Bhawna")
```

---

## 6. `**kwargs` – Variable Keyword Arguments
**Theory:** `**kwargs` allows a function to accept **any number of keyword arguments**. Inside the function, they are stored as a **dictionary**.

```python
def student_details(**info):
    print(type(info))          # <class 'dict'>
    for key, value in info.items():
        print(f"{key}: {value}")

student_details(name="Bhawna", age=21, course="Python", city="Ludhiana")

def calculate_total(**prices):
    total = sum(prices.values())
    print("Items:", prices)
    print("Total:", total)

calculate_total(shirt=500, pants=800, shoes=1200)
```

---

## 7. Mixing All Types of Arguments
**Theory:** Order rule when mixing — `positional → *args → keyword → **kwargs`

```python
def show_all(name, *subjects, city="Ludhiana", **extra):
    print(f"Name: {name}")
    print(f"Subjects: {subjects}")
    print(f"City: {city}")
    print(f"Extra Info: {extra}")

show_all("Bhawna", "Python", "DSA", "ML", city="Delhi", age=21, batch="Morning")
```

---

## 8. Recursion (Brief Theory)
**Theory:** Recursion is when a function **calls itself** to solve a smaller version of the same problem. Every recursive function must have:
- **Base case** → condition where recursion stops
- **Recursive case** → function calling itself with reduced input

```
factorial(5)
= 5 * factorial(4)
= 5 * 4 * factorial(3)
= 5 * 4 * 3 * factorial(2)
= 5 * 4 * 3 * 2 * factorial(1)
= 5 * 4 * 3 * 2 * 1
= 120
```

---

## 9. Recursion – Practical Programs

### Factorial
```python
def factorial(n):
    if n == 0 or n == 1:   # base case
        return 1
    return n * factorial(n - 1)

print(factorial(5))    # 120
print(factorial(6))    # 720
```

### Fibonacci Series
```python
def fibonacci(n):
    if n <= 0:
        return 0
    if n == 1:
        return 1
    return fibonacci(n - 1) + fibonacci(n - 2)

for i in range(8):
    print(fibonacci(i), end=" ")
# 0 1 1 2 3 5 8 13
```

### Sum of Natural Numbers
```python
def natural_sum(n):
    if n == 0:
        return 0
    return n + natural_sum(n - 1)

print(natural_sum(10))    # 55
```

### Power (a raised to b)
```python
def power(base, exp):
    if exp == 0:
        return 1
    return base * power(base, exp - 1)

print(power(2, 10))    # 1024
```

### Reverse a String
```python
def reverse_string(s):
    if len(s) == 0:
        return ""
    return s[-1] + reverse_string(s[:-1])

print(reverse_string("Bhawna"))    # anwahB
```

### Check Palindrome using Recursion
```python
def is_palindrome(s):
    if len(s) <= 1:
        return True
    if s[0] != s[-1]:
        return False
    return is_palindrome(s[1:-1])

print(is_palindrome("madam"))    # True
print(is_palindrome("Bhawna"))   # False
```

### Count Elements in a List Recursively
```python
def count_elements(lst):
    if lst == []:
        return 0
    return 1 + count_elements(lst[1:])

print(count_elements([10, 20, 30, 40, 50]))    # 5
```

---

## 10. Recursion vs Iteration

| Feature | Recursion | Iteration |
|---|---|---|
| Syntax | Cleaner, shorter | Longer but explicit |
| Memory | Uses call stack (more memory) | Less memory |
| Speed | Slower for large inputs | Faster |
| Best for | Trees, factorial, fibonacci | Loops, simple counting |

---

## Summary of Day 7
Today I learned all **5 types of function arguments** — positional (order matters), keyword (name-based), default (fallback value), `*args` (accepts any number of values as tuple), and `**kwargs` (accepts any number of keyword values as dict). I also practiced **recursion** — a function calling itself with a base case to stop — through programs like factorial, fibonacci, power, reverse string, palindrome check, and list counting.

