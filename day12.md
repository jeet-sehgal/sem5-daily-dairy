# Daily Diary – Day 12
`Date : 6/7/26`
**Subject:** Python Programming
#### **Topic Covered:** Revision & Practice – Loops, Strings, Functions, Recursion, OOP (Inheritance)

---

## 1. Loops – Practical Practice

### Print numbers 1 to 10
```python
for i in range(1, 11):
    print(i)
# Output: 1 2 3 4 5 6 7 8 9 10
```

### Print even numbers from 2 to 20
```python
for i in range(2, 21, 2):
    print(i)
# Output: 2 4 6 8 10 12 14 16 18 20
```

### Print odd numbers from 1 to 20
```python
for i in range(1, 21, 2):
    print(i)
# Output: 1 3 5 7 9 11 13 15 17 19
```

### Sum of first 100 natural numbers (Formula)
```python
print(100 * (100 + 1) / 2)
# Output: 5050.0
```

### Multiplication table of 3
```python
for i in range(11):
    print("3 X", i, "=", 3 * i)
# Output:
# 3 X 0 = 0
# 3 X 1 = 3
# 3 X 2 = 6
# ...
# 3 X 10 = 30
```

---

## 2. Strings – Reversal & Palindrome

### Reverse a string
```python
print("100"[::-1])    # Output: 001

print(len("100"))     # Output: 3
```

### Palindrome check using ternary operator
**Theory:** A **palindrome** is a string/number that reads the same forwards and backwards.

```python
print("palindrome" if "1001"[::-1] == "1001" else "Not Palindrome")
# Output: palindrome

# More examples
print("palindrome" if "madam"[::-1] == "madam" else "Not Palindrome")   # palindrome
print("palindrome" if "hello"[::-1] == "hello" else "Not Palindrome")   # Not Palindrome
```

---

## 3. While Loop with Break

**Theory:** `while True` creates an infinite loop. `break` exits the loop when a condition is met.

```python
while True:
    a = input("Enter: ")
    if a == "0":
        break
# Loop keeps asking for input until user enters "0"
```

---

## 4. Functions – Revision

### Basic function with parameter
```python
def bhai(c):
    print(c)

bhai("Hello")    # Output: Hello
```

### Function with return value
```python
def add(a, b):
    return a + b

print(add(5, 3))    # Output: 8
```

### Function with conditional logic
```python
def even_odd(n):
    if n % 2 == 0:
        print("Even")
    else:
        print("Odd")

even_odd(5)    # Output: Odd
even_odd(4)    # Output: Even
```

### max() with a list
```python
print(max([1, 2, 3, 4, 5, 44, 22]))    # Output: 44
```

---

## 5. Recursion – Factorial

**Theory:** A recursive function calls itself with a smaller input. The **base case** stops the recursion.

```python
def factorial(n):
    if n == 0:          # base case
        return 1
    else:
        return n * factorial(n - 1)

factorial(5)    # 5 * 4 * 3 * 2 * 1 = 120
```

**Trace of `factorial(5)`:**
```
factorial(5) = 5 * factorial(4)
             = 5 * 4 * factorial(3)
             = 5 * 4 * 3 * factorial(2)
             = 5 * 4 * 3 * 2 * factorial(1)
             = 5 * 4 * 3 * 2 * 1 * factorial(0)
             = 5 * 4 * 3 * 2 * 1 * 1
             = 120
```

---

## 6. OOP – Single Inheritance Revision

**Theory:** Child class inherits parent class attributes and methods. `super()` is used to call the parent's `__init__` and methods.

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def display(self):
        print("Name:", self.name)
        print("Age:", self.age)

class Employee(Person):
    def __init__(self, name, age, salary):
        super().__init__(name, age)    # call Person's __init__
        self.salary = salary

    def display(self):
        super().display()              # call Person's display()
        print("Salary:", self.salary)

emp = Employee("John", 30, 50000)
emp.display()

# Output:
# Name: John
# Age: 30
# Salary: 50000
```

---

## 7. Class with Attributes (No Inheritance)

```python
class Shape:
    def __init__(self, sides):
        self.sides = sides

circle = Shape(0)        # circle has 0 sides
rectangle = Shape(4)     # rectangle has 4 sides

print(circle.sides)      # 0
print(rectangle.sides)   # 4
```

---

## 8. Full Practice Program – Combining All
```python
# Function + Loop + Condition
def print_table(n):
    for i in range(11):
        print(f"{n} X {i} = {n * i}")

print_table(5)

# Palindrome function
def is_palindrome(s):
    return "Palindrome" if str(s)[::-1] == str(s) else "Not Palindrome"

print(is_palindrome("madam"))   # Palindrome
print(is_palindrome(121))       # Palindrome
print(is_palindrome("hello"))   # Not Palindrome

# Factorial using recursion
def factorial(n):
    if n == 0:
        return 1
    return n * factorial(n - 1)

print(factorial(6))    # 720

# Class with inheritance
class Animal:
    def __init__(self, name):
        self.name = name
    def speak(self):
        print(f"{self.name} makes a sound")

class Dog(Animal):
    def speak(self):
        print(f"{self.name} says Woof!")

d = Dog("Tommy")
d.speak()    # Tommy says Woof!
```

---

## Summary of Day 12
Today was a **revision and practice day** covering all previously learned concepts. I practiced `for` loops with `range()` (step values for even/odd), string reversal using slicing `[::-1]`, palindrome check using ternary operator, `while True` with `break` for user input, functions (with and without return), `max()` on lists, **recursion** for factorial, and **OOP** with single inheritance using `super()` to call parent constructors and methods.

**Key Concepts Revised:**

| Topic | Key Point |
|---|---|
| `range(start, stop, step)` | Controls loop increment |
| `s[::-1]` | Reverses any string/list |
| Palindrome | Reversed == Original |
| `while True` + `break` | Infinite loop with exit condition |
| `super().__init__()` | Calls parent constructor |
| Recursion | Function calls itself; needs base case |