# Daily Diary – Day 3
`Date :- 24/6/26`

**Subject:** Python Programming
#### **Topic Covered:** Python Data Types – Lists, Tuples, Sets, Dictionary

---

## 1. Lists (Brief Theory)
A **list** stores multiple items in a single variable using `[ ]`. Lists are **ordered, mutable (changeable), heterogeneous, and allow duplicates**.

```python
FRUITS = ["apple", "banana", "cherry", 24, 78.90, True, ["ram", "sham"]]
print(FRUITS)

my_list = ["apple", "banana", "cherry", "apple", "cherry"]   # duplicates allowed
print(len(my_list))                                          # length of list

thislist = list(("apple", "banana", "cherry"))                # list() constructor
print(thislist)
```

### List Methods – Practical
```python
UNI = ["CTU", "KTU", "DTU"]
UNI.append("CU")                 # add element at end
print(UNI)

Courses = ["BCA", "MCA"]
UNI.append(Courses)              # nested list
print(UNI)

UNI.clear()                      # empty the list
print(UNI)

UNI = ["CTU", "KTU", "DTU"]
colleges = UNI.copy()            # copy a list
print(colleges)

UNI = ["CTU", "KTU", "DTU", "CTU"]
print(UNI.count("CTU"))          # count occurrences

UNI2 = ["CU", "PU"]
UNI2.extend(UNI)                 # merge two lists
print(UNI2)

print(UNI2.index("KTU"))         # index of first occurrence
UNI2.insert(1, "PUNJABI UNIVERSITY")   # insert at index
print(UNI2)

FUR = ["TABLE", "CHAIR", "STOOL", "BED"]
FUR.pop()                        # remove last item
FUR.pop(0)                       # remove item at index 0
print(FUR)

FUR = ["TABLE", "CHAIR", "STOOL", "BED"]
FUR.remove("CHAIR")              # remove by value
print(FUR)

FUR.reverse()                    # reverse list
print(FUR)

FUR.sort()                       # sort ascending
print(FUR)
print(sorted(FUR))               # sorted() returns new list
FUR.sort(reverse=True)           # sort descending
print(FUR)
```

### List Slicing
```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9]
print(numbers[2:6])     # [3, 4, 5, 6]
print(numbers[:4])      # [1, 2, 3, 4]
print(numbers[5:])      # [6, 7, 8, 9]
print(numbers[-5:])     # last 5 elements
print(numbers[::2])     # every 2nd item
print(numbers[::-1])    # reversed list
```

---

## 2. Tuples (Brief Theory)
A **tuple** is an ordered, **immutable** collection created with `()`. Once created, elements cannot be changed.

```python
fruits = ('apple', 'orange', 'banana')
single_element_tuple = ("42",)          # comma needed for single element
mytuple = tuple(("apple", "banana", "cherry"))  # tuple() constructor

print(fruits[1])                        # accessing -> 'orange'

City = ("DELHI", "MUMBAI", "KOTA", "LUDHIANA")
if "LUDHIANA" in City:
    print("Yes, LUDHIANA is in the city tuple")

# Immutability - workaround using list conversion
Country = ("INDIA", "SRI LANKA", "AMERICA")
y = list(Country)
y[1] = "BANGLADESH"
X = tuple(y)
print(X)

Tuple1 = (0, 1, 2, 3, 2, 3, 1, 3, 2)
print(Tuple1.count(3))          # count occurrences
print(Tuple1.index(3))          # index of first occurrence

numbers = (1, 2, 3, 4, 5)
print(numbers[::-1])            # reverse a tuple
```

---

## 3. Sets (Brief Theory)
A **set** is an unordered collection of **unique, immutable** elements created with `{ }`. Duplicates are automatically removed. A **frozenset** is an immutable version of a set.

```python
basket = {'apple', 'orange', 'apple', 'pear', 'orange', 'banana'}
print(basket)                  # duplicates removed

b = frozenset('asdfagsa')      # frozenset example
print(b)

# Set operations
a, b = {1, 2, 3, 4, 5}, {3, 4, 5, 6}
print(a.intersection(b))       # {3, 4, 5}
print(a.union(b))              # union
print(a.difference(b))         # elements only in a
print(a.symmetric_difference(b))  # elements not common to both

print({1, 2}.issubset({1, 2, 3}))     # True
print({1, 2}.issuperset({1, 2, 3}))   # False
print({1, 2}.isdisjoint({3, 4}))      # True

s = {1, 2, 3}
s.add(4); print(s)
s.discard(3); print(s)
s.remove(1); print(s)
s.update({5, 6}); print(s)

# Removing duplicates from a list using a set
restaurants = ["McDonald's", "Burger King", "McDonald's", "Chicken Chicken"]
print(set(restaurants))
print(list(set(restaurants)))
```

---

## 4. Dictionary (Brief Theory)
A **dictionary** stores data as **key:value** pairs inside `{ }`. Keys must be unique and immutable (string, number, or tuple); values can be any data type.

```python
dis = {'name': 'red', 'age': 10}
print(dis)
print(dis['name'])             # access value by key
print(list(dis.values()))      # all values
print(dis.keys())              # all keys

# Creating dictionaries
d = dict(Name='Diksha')
d = dict([('Name', 'Diksha'), ('Age', '21')])
print(d)

# Modifying
d['H.No'] = 42                 # add new key-value pair
d['new_list'] = [1, 2, 3]
print(d)
del d['H.No']                  # delete a key

# Built-in dictionary methods
d = {'Name': 'Ram', 'Age': '19', 'Country': 'India'}
print(d.get('Name'))           # safe access -> Ram
print(d.get('Gender'))         # not present -> None
print(d.items())               # key-value pairs
print(d.keys())
print(list(d.values()))

d1 = {'Name': 'Ram', 'Age': '19'}
d2 = {'Name': 'Neha', 'Age': '22'}
d1.update(d2)                  # merge/update dict
print(d1)

d.pop('Age')                   # remove key & return value
print(d)

d.popitem()                    # remove last inserted item
print(d)

d.clear()                      # empty the dictionary
print(d)
```

---

## 5. Practice Program – Combining All
```python
# Mixed data types in a list
mixed = [{1, 2, 3}, {'name': 'Bhawna'}, ['a', 'b'], (10, 20)]
print(mixed[0])    # set
print(mixed[1])    # dict
print(mixed[2])    # list
print(mixed[3])    # tuple

# Practice: unique elements + dict mapping
fruits_list = ["apple", "banana", "apple", "mango"]
unique_fruits = set(fruits_list)
fruit_count = {fruit: fruits_list.count(fruit) for fruit in unique_fruits}
print(fruit_count)
```

---

## Summary of Day 3
Today I learned about all **4 collection data types in Python** — Lists, Tuples, Sets, and Dictionaries. I practiced list methods (`append`, `insert`, `pop`, `sort`, slicing), tuple immutability and its methods (`count`, `index`), set operations (`union`, `intersection`, `difference`), and dictionary methods (`get`, `update`, `pop`, `items`). I also understood when to use which data type based on mutability, order, and uniqueness requirements.

**Practice Questions for Tomorrow:**
1. Create a list of 5 fruits, sort it, then reverse it.
2. Create a tuple of 3 colors and try to modify it — note the error.
3. Use sets to find common elements between two friend-group lists.
4. Create a dictionary of student records and update one record.
5. Convert a list with duplicate values into a set, then back into a list.