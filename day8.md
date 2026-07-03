# Daily Diary – Day 8
`Date : 1/8/26`
**Subject:** Python Programming
#### **Topic Covered:** `map()`, `filter()`, Closures & Nested Functions

---

## 1. `map()` Function (Brief Theory)
`map()` applies a function to **every element** of an iterable (list, tuple, etc.) and returns a map object. Convert it to a list to see the result.

**Syntax:** `map(function, iterable)`

```python
# Without map - using loop
numbers = [1, 2, 3, 4, 5]
squared = []
for n in numbers:
    squared.append(n ** 2)
print(squared)     # [1, 4, 9, 16, 25]

# With map - much cleaner
def square(n):
    return n ** 2

numbers = [1, 2, 3, 4, 5]
result = list(map(square, numbers))
print(result)      # [1, 4, 9, 16, 25]
```

### `map()` with lambda (one-liner)
```python
numbers = [1, 2, 3, 4, 5]
print(list(map(lambda x: x ** 2, numbers)))         # [1, 4, 9, 16, 25]
print(list(map(lambda x: x * 2, numbers)))          # [2, 4, 6, 8, 10]
print(list(map(lambda x: x + 10, numbers)))         # [11, 12, 13, 14, 15]
```

### `map()` with strings
```python
names = ["bhawna", "taman", "ram", "sham"]
print(list(map(str.upper, names)))                  # ['BHAWNA', 'TAMAN', 'RAM', 'SHAM']
print(list(map(str.capitalize, names)))             # ['Bhawna', 'Taman', 'Ram', 'Sham']
print(list(map(len, names)))                        # [6, 5, 3, 4]
```

### `map()` with two lists
```python
a = [1, 2, 3, 4]
b = [10, 20, 30, 40]
result = list(map(lambda x, y: x + y, a, b))
print(result)      # [11, 22, 33, 44]
```

### Practical – Convert string numbers to integers
```python
str_numbers = ["10", "20", "30", "40", "50"]
int_numbers = list(map(int, str_numbers))
print(int_numbers)                                  # [10, 20, 30, 40, 50]
print(sum(int_numbers))                             # 150
```

---

## 2. `filter()` Function (Brief Theory)
`filter()` applies a function that returns `True` or `False` to each element of an iterable and **keeps only elements where the result is True**.

**Syntax:** `filter(function, iterable)`

```python
# Without filter - using loop
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
even = []
for n in numbers:
    if n % 2 == 0:
        even.append(n)
print(even)        # [2, 4, 6, 8, 10]

# With filter - much cleaner
def is_even(n):
    return n % 2 == 0

numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
result = list(filter(is_even, numbers))
print(result)      # [2, 4, 6, 8, 10]
```

### `filter()` with lambda
```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

evens   = list(filter(lambda x: x % 2 == 0, numbers))
odds    = list(filter(lambda x: x % 2 != 0, numbers))
greater = list(filter(lambda x: x > 5, numbers))

print("Evens:", evens)      # [2, 4, 6, 8, 10]
print("Odds:", odds)        # [1, 3, 5, 7, 9]
print("Greater than 5:", greater)  # [6, 7, 8, 9, 10]
```

### `filter()` with strings
```python
names = ["Ram", "Sham", "Bhawna", "Taman", "Gita", "Bo"]
long_names = list(filter(lambda name: len(name) > 3, names))
print(long_names)           # ['Sham', 'Bhawna', 'Taman', 'Gita']
```

### Practical – Filter passing students
```python
students = [
    {"name": "Bhawna", "marks": 85},
    {"name": "Taman", "marks": 28},
    {"name": "Ram", "marks": 72},
    {"name": "Sham", "marks": 30},
    {"name": "Gita", "marks": 90},
]

passed = list(filter(lambda s: s["marks"] >= 33, students))
for s in passed:
    print(f"{s['name']} - {s['marks']}")
```

---

## 3. Combining `map()` and `filter()`
```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Step 1: filter even numbers
# Step 2: square only the even ones
result = list(map(lambda x: x ** 2, filter(lambda x: x % 2 == 0, numbers)))
print(result)      # [4, 16, 36, 64, 100]
```

---

## 4. `map()` vs `filter()` – Key Difference

| Feature | `map()` | `filter()` |
|---|---|---|
| Purpose | Transform every element | Select specific elements |
| Output size | Same as input | Equal to or smaller than input |
| Function returns | Transformed value | True / False |
| Example | square each number | keep only even numbers |

---

## 5. Nested Functions (Brief Theory)
**Theory:** A function defined **inside another function** is called a nested or inner function. It can access variables of the outer function.

```python
def outer():
    msg = "Hello from outer!"

    def inner():
        print(msg)      # inner can access outer's variable

    inner()

outer()
```

---

## 6. Closures (Brief Theory)
**Theory:** A **closure** is a nested function that **remembers the variables of its outer function even after the outer function has finished executing**. The inner function "closes over" the outer variable.

3 conditions for a closure:
1. There must be a nested function
2. The inner function must refer to a value from the outer function
3. The outer function must return the inner function

```python
def outer_function(msg):
    def inner_function():
        print(f"Message: {msg}")    # remembers msg even after outer is done
    return inner_function           # return function, not calling it

greet = outer_function("Hello, Bhawna!")
greet()                             # Message: Hello, Bhawna!

# msg is no longer in scope, but closure remembers it
greet2 = outer_function("Good Morning!")
greet2()                            # Message: Good Morning!
```

### Closure – Counter Example
```python
def make_counter():
    count = 0
    def counter():
        nonlocal count              # modify outer variable
        count += 1
        print(f"Count: {count}")
    return counter

c1 = make_counter()
c1()    # Count: 1
c1()    # Count: 2
c1()    # Count: 3

c2 = make_counter()     # independent counter
c2()    # Count: 1
```

### Closure – Multiplier Factory
```python
def multiplier(factor):
    def multiply_by(number):
        return number * factor
    return multiply_by

double = multiplier(2)
triple = multiplier(3)
times10 = multiplier(10)

print(double(5))     # 10
print(triple(5))     # 15
print(times10(5))    # 50
```

### Closure – Discount Calculator
```python
def discount_calculator(discount_percent):
    def apply_discount(price):
        discount = price * discount_percent / 100
        return price - discount
    return apply_discount

student_discount = discount_calculator(10)
diwali_discount  = discount_calculator(25)
clearance_sale   = discount_calculator(50)

print(f"Original: 1000 -> After Student Discount: {student_discount(1000)}")
print(f"Original: 1000 -> After Diwali Discount:  {diwali_discount(1000)}")
print(f"Original: 1000 -> After Clearance Sale:   {clearance_sale(1000)}")
```

---

## 7. Practice Program – Combining All
```python
# Student marks list
marks = [45, 82, 29, 91, 33, 15, 76, 55, 38, 60]

# Step 1: filter passing students (>=33)
passed_marks = list(filter(lambda m: m >= 33, marks))

# Step 2: add 5 bonus marks to each passer using map
bonus_marks = list(map(lambda m: m + 5, passed_marks))

# Step 3: closure to check grade
def grade_checker(threshold):
    def check(mark):
        if mark >= threshold:
            return f"{mark} -> PASS"
        return f"{mark} -> FAIL"
    return check

is_above_60 = grade_checker(60)
final_result = list(map(is_above_60, bonus_marks))

for r in final_result:
    print(r)
```

---

## Summary of Day 8
Today I learned `map()` (applies a function to every element), `filter()` (keeps elements where the function returns `True`), and how to combine both for clean, readable data processing. I also learned **nested functions** (function inside a function) and **closures** — a powerful concept where the inner function remembers the outer function's variables even after the outer function has finished. Closures are used to build factories like counter, multiplier, and discount calculator.

**Practice Questions for Tomorrow:**
1. Use `map()` to convert a list of temperatures from Celsius to Fahrenheit.
2. Use `filter()` to get all words longer than 5 characters from a list of words.
3. Combine `map()` and `filter()` to get squares of odd numbers from 1 to 20.
4. Write a closure that works as a greeting generator (takes a language and returns a greeting function).
5. Write a closure-based `power_factory(exp)` that returns functions like `square`, `cube` etc.