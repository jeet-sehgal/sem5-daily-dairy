# Daily Diary – Day 5
`Date: 26/6/26`

**Subject:** Python Programming
#### **Topic Covered:** User-Defined Functions (in depth) & Lists (functions with lists, list comprehension)

---

## 1. User-Defined Functions – Recap (Brief Theory)
A function is a block of reusable code defined with `def`, called by its name. Functions can take **parameters**, return values using `return`, and can be combined with data structures like lists.

```python
def square(num):
    return num * num

print(square(5))     # 25
```

## 2. Passing a List to a Function
**Theory:** Lists can be passed as arguments to functions. Since lists are mutable, changes made inside the function affect the original list.

```python
def display_list(items):
    for item in items:
        print(item)

fruits = ["apple", "banana", "cherry"]
display_list(fruits)

# Modifying a list inside a function (mutable effect)
def add_item(items, new_item):
    items.append(new_item)

numbers = [1, 2, 3]
add_item(numbers, 4)
print(numbers)        # [1, 2, 3, 4] -> original list changed
```

## 3. Function Returning a List
```python
def get_even_numbers(numbers):
    even_list = []
    for n in numbers:
        if n % 2 == 0:
            even_list.append(n)
    return even_list

nums = [1, 2, 3, 4, 5, 6, 7, 8]
print(get_even_numbers(nums))     # [2, 4, 6, 8]
```

## 4. Function with Default & Variable Arguments using Lists
```python
def total_marks(*marks):
    return sum(marks)

print(total_marks(80, 90, 70, 85))   # 325

def average_marks(marks=[]):
    if len(marks) == 0:
        return 0
    return sum(marks) / len(marks)

print(average_marks([80, 90, 70, 85]))  # 81.25
```

---

## 5. Common List Operations Inside Functions
```python
def find_max(numbers):
    return max(numbers)

def find_min(numbers):
    return min(numbers)

def reverse_list(numbers):
    return numbers[::-1]

def sort_list(numbers, descending=False):
    return sorted(numbers, reverse=descending)

data = [12, 45, 7, 23, 56, 3]
print("Max:", find_max(data))
print("Min:", find_min(data))
print("Reversed:", reverse_list(data))
print("Sorted Ascending:", sort_list(data))
print("Sorted Descending:", sort_list(data, True))
```

## 6. Function to Remove Duplicates from a List
```python
def remove_duplicates(items):
    return list(set(items))

names = ["Ram", "Sham", "Ram", "Gita", "Sham"]
print(remove_duplicates(names))
```

## 7. Function for Searching in a List
```python
def search_item(items, target):
    if target in items:
        return f"{target} found at index {items.index(target)}"
    else:
        return f"{target} not found in the list"

cities = ["Delhi", "Mumbai", "Ludhiana", "Kota"]
print(search_item(cities, "Ludhiana"))
print(search_item(cities, "Chandigarh"))
```

---

## 8. List Comprehension with Functions (Brief Theory)
**Theory:** List comprehension is a short way of creating a list using a single line of code, often combined with functions.

```python
def cube(n):
    return n ** 3

cubes = [cube(x) for x in range(1, 6)]
print(cubes)               # [1, 8, 27, 64, 125]

# List comprehension with condition
even_squares = [x**2 for x in range(1, 11) if x % 2 == 0]
print(even_squares)        # [4, 16, 36, 64, 100]
```

---

## 9. Practice Program – Combining Functions & Lists
```python
def process_marks(marks):
    highest = max(marks)
    lowest = min(marks)
    avg = sum(marks) / len(marks)
    passed = [m for m in marks if m >= 33]
    return highest, lowest, avg, passed

student_marks = [45, 78, 12, 90, 33, 25, 67]
high, low, avg, passed_list = process_marks(student_marks)

print("Highest:", high)
print("Lowest:", low)
print("Average:", avg)
print("Passed Students Marks:", passed_list)
```

---

## Summary of Day 5
Today I learned how **user-defined functions work together with lists** — passing lists as arguments, modifying them inside functions (mutability), returning new lists, and using built-in list functions like `max()`, `min()`, `sorted()`, and `set()` inside custom functions. I also practiced **list comprehension** as a compact alternative to loops for building lists.

