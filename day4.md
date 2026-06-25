# Daily Diary – Day 4
`Date : 25/6/26` 
**Subject:** Python Programming
#### **Topic Covered:** User-Defined Functions, Classes & Objects, `__init__` Method, Single Inheritance, Multilevel Inheritance

---

## 1. User-Defined Functions (Brief Theory)
A **function** is a reusable block of code that performs a specific task, defined using the `def` keyword. Functions help avoid repetition and make code organized.

```python
# Simple function
def greet():
    print("Hello, welcome to Python class!")

greet()

# Function with parameters
def add_numbers(a, b):
    return a + b

print(add_numbers(5, 10))   # 15

# Function with default parameter
def greet_person(name="Student"):
    print(f"Hello, {name}!")

greet_person()              # Hello, Student!
greet_person("Bhawna")      # Hello, Bhawna!

# Function with multiple return values
def calculate(a, b):
    return a + b, a - b, a * b, a / b

s, d, m, dv = calculate(10, 5)
print(s, d, m, dv)

# Function with *args (variable number of arguments)
def total_sum(*numbers):
    return sum(numbers)

print(total_sum(1, 2, 3, 4, 5))   # 15

# Function with **kwargs (keyword arguments)
def student_info(**details):
    for key, value in details.items():
        print(f"{key}: {value}")

student_info(name="Bhawna", age=21, course="Python")
```

---

## 2. Classes and Objects (Brief Theory)
A **class** is a blueprint for creating objects. An **object** is an instance of a class that has its own data (attributes) and behavior (methods).

```python
class Student:
    pass

s1 = Student()          # creating an object
s1.name = "Bhawna"
s1.age = 21
print(s1.name, s1.age)
```

## 3. The `__init__` Method
**Theory:** `__init__` is a special **constructor** method, automatically called when an object is created. It is used to initialize attributes of the object. `self` refers to the current object.

```python
class Student:
    def __init__(self, name, age, course):
        self.name = name
        self.age = age
        self.course = course

    def display(self):
        print(f"Name: {self.name}, Age: {self.age}, Course: {self.course}")

s1 = Student("Bhawna", 21, "Python")
s2 = Student("Taman", 22, "Java")

s1.display()
s2.display()
```

---

## 4. Single Inheritance
**Theory:** When a class (**child/derived class**) inherits properties and methods from one parent class (**base class**), it is called single inheritance.

```python
# Parent class
class Animal:
    def __init__(self, name):
        self.name = name

    def eat(self):
        print(f"{self.name} is eating.")

    def sleep(self):
        print(f"{self.name} is sleeping.")

# Child class
class Dog(Animal):
    def bark(self):
        print(f"{self.name} is barking.")

d1 = Dog("Tommy")
d1.eat()      # inherited method
d1.sleep()    # inherited method
d1.bark()     # own method
```

## 5. Multilevel Inheritance
**Theory:** When a class inherits from a child class, which itself inherits from a parent class, forming a chain (grandparent → parent → child).

```python
# Grandparent class
class Animal:
    def __init__(self, name):
        self.name = name

    def eat(self):
        print(f"{self.name} is eating.")

# Parent class
class Dog(Animal):
    def bark(self):
        print(f"{self.name} is barking.")

# Child class
class Puppy(Dog):
    def weep(self):
        print(f"{self.name} is weeping.")

p1 = Puppy("Bruno")
p1.eat()     # from Animal (grandparent)
p1.bark()    # from Dog (parent)
p1.weep()    # own method
```

---

## 6. Using `super()` with Inheritance
**Theory:** `super()` is used inside a child class to call the constructor/methods of its parent class.

```python
class Animal:
    def __init__(self, name):
        self.name = name
        print(f"{self.name} is an animal.")

class Dog(Animal):
    def __init__(self, name, breed):
        super().__init__(name)     # calling parent constructor
        self.breed = breed
        print(f"{self.name} is a {self.breed}.")

d1 = Dog("Tommy", "Labrador")
```

---

## 7. Practice Program – Combining Functions & OOP
```python
class Employee:
    def __init__(self, name, salary):
        self.name = name
        self.salary = salary

    def show_details(self):
        print(f"Employee: {self.name}, Salary: {self.salary}")

class Manager(Employee):
    def __init__(self, name, salary, department):
        super().__init__(name, salary)
        self.department = department

    def show_details(self):
        super().show_details()
        print(f"Department: {self.department}")

class SeniorManager(Manager):
    def __init__(self, name, salary, department, team_size):
        super().__init__(name, salary, department)
        self.team_size = team_size

    def show_details(self):
        super().show_details()
        print(f"Team Size: {self.team_size}")

sm = SeniorManager("Bhawna", 85000, "IT", 12)
sm.show_details()
```

---

## Summary of Day 4
Today I learned about **user-defined functions** (with parameters, default values, `*args`, and `**kwargs`) and the basics of **Object-Oriented Programming** in Python. I understood how `class` and `__init__` work together to create objects with attributes, and practiced **single inheritance** (one parent → one child) and **multilevel inheritance** (grandparent → parent → child chain), along with using `super()` to access parent class members.
