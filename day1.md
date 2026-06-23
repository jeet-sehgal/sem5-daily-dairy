# Daily Diary – Day 1
`Date - 22/6/2026`

**Subject:** Python Programming
**Topic Covered:** Introduction to Python, Syntax, Print Statement, Variables, Data Types, Type Casting, Input Function, Swapping & Unpacking of Variables

---

## 1. Introduction to Python (Brief Theory)
- Python is a high-level, interpreted, general-purpose programming language created by **Guido van Rossum in 1991**.
- It is easy to read/write, case-sensitive, and executed line by line (interpreted).
- Used widely in web development, data science, AI, and automation.

## 2. Python Syntax
- Indentation defines code blocks (no `{}` like other languages).
- No semicolons `;` needed at the end of statements.
- `#` is used for comments.

---

## 3. Practical Work – `print()` Statement
```python
print("Bhawna")                   # double quotation
print('how are you guysss')       # single quotation
print(00000000)
print(1222+45655)
print(12*12)
print(4511-6544)
print(32/2)
```

## 4. Variables
**Theory:** Variables store data values. They must start with a letter/underscore, can contain letters/numbers/underscores, are case-sensitive, and are **dynamically typed** (no need to declare type).

```python
name = "Bhawna"     # valid
_age = 21            # valid
Age = 23             # different from age (case-sensitive)

a, b = 21, "taman"
print(f'value of number is {a} and string is {b}')

a = 10
b = 20
print(a > b)         # False

a = 200
b = a
print(b)             # 200
```

## 5. Data Types
**Theory:** Common built-in types: `int`, `float`, `str`, `bool`.

```python
a = True
print(a)             # bool

a = 4545
b = 74.44
c = False
d = "sdfghj"
print(a, b, c, d)

# type() function -> finds data type
print(type(a))
print(type(b))
print(type(c))
print(type(d))
```

## 6. Input Function
**Theory:** `input()` takes user input (always returns string by default; cast it as needed).

```python
a = str(input("Enter your name: "))
print(a)

a = int(input("Enter a number: "))
b = float(input("Enter a number: "))
c = bool(input("Enter a value: "))
d = str(input("Enter a name: "))
print(a, b, c, d)
```

## 7. Type Casting
**Theory:** Converting one data type into another (`int()`, `float()`, `str()`, `bool()`).

```python
a = 10
print(float(a))      # int -> float

a = "25"
print(int(a))        # string -> int

a = 5.8
print(int(a))        # float -> int

a = "12"
print(float(a))      # string -> float

a = 233.777
print(str(a))        # int/float -> string
print(type(a))
```

## 8. Swapping Variables
**Theory:** Exchanging values of two variables — three methods.

```python
# Using tuple unpacking
a, b = 21, 67
a, b = b, a
print(a, b)

# Using third variable
a, b = 5, 10
temp = a
a = b
b = temp
print(a, b)

```

## 9. Unpacking Variables
**Theory:** Assigning values from a list/tuple to multiple variables in one line.

```python
numbers = [1, 2, 3, 4]
a, b, c, d = numbers
print(a, b, c, d)

a = [1, 4, 67, 7]
print(max(a))
print(min(a))
print(sum(a))
```

---

## 10. Practice Questions Solved Today
```python
# 1. Print Hello World
print("Hello World")

# 2. Print name and age separately
print("Bhawna")
print(21)

# 3. Store two numbers and print their sum
a, b = 3, 6
print(a + b)

# 4. Store a string and print it with its data type
a = "Bhawna"
print(a, type(a))

# 5. Convert string number to int and add 20
ab = "50"
print(int(ab) + 20)

# 6. Take age and print age after 5 years
age = int(input("Enter your age: "))
print(age + 5)

# 7. Area of rectangle using input
length = int(input("Enter length: "))
width = int(input("Enter width: "))
print(length * width)

# 8. Swap two numbers taken from user
a = int(input("Enter first number: "))
b = int(input("Enter second number: "))
a, b = b, a
print(a, b)

# 9. Multiple variable assignment using unpacking
a, b, c = 5, 10, 15
print(a, b, c)

# 10. Square of a number
a = int(input("Enter a number: "))
print("Square:", a * a)
```

---

## Summary of Day 1
Today I learned the basics of Python — its history, syntax rules, and how to use `print()` and `input()`. I practiced declaring variables, checked their data types using `type()`, performed type casting between `int`, `float`, `str`, and `bool`, and solved problems on **swapping** and **unpacking** variables using multiple methods.

**Homework Practice Questions:**
1. Print "Hello World".
2. Print your name.
3. Print two lines using two `print()` statements.
4. Print numbers from 1 to 3.
5. Print your school name.
6. Print any message inside double quotes.
7. Print the sum of two numbers.