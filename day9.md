# Daily Diary – Day 9
`date : 2/7/26`
**Subject:** Python Programming
#### **Topic Covered:** Object-Oriented Programming (OOPs) – All Concepts in Brief

---

## 1. What is OOP? (Brief Theory)
OOP is a programming approach that organizes code around **objects** rather than functions. Everything in Python is an object.

**4 Pillars of OOP:**
| Pillar | Meaning |
|---|---|
| Encapsulation | Wrapping data and methods together, hiding internal details |
| Abstraction | Hiding complexity, showing only essential features |
| Inheritance | Child class acquiring properties of parent class |
| Polymorphism | Same method name, different behavior |

---

## 2. Class & Object
**Theory:** A **class** is a blueprint; an **object** is a real instance created from that blueprint.

```python
class Car:
    brand = "Toyota"          # class variable (shared by all objects)

    def __init__(self, model, price):
        self.model = model    # instance variable (unique to each object)
        self.price = price

    def display(self):
        print(f"Brand: {Car.brand}, Model: {self.model}, Price: {self.price}")

c1 = Car("Fortuner", 3500000)
c2 = Car("Innova", 2000000)

c1.display()
c2.display()
print(Car.brand)     # accessing class variable
```

---

## 3. `__init__` & `self`
**Theory:** `__init__` is the **constructor** — called automatically when an object is created. `self` refers to the current object instance.

```python
class Student:
    def __init__(self, name, age, marks):
        self.name = name
        self.age = age
        self.marks = marks

    def result(self):
        if self.marks >= 33:
            print(f"{self.name} -> PASS")
        else:
            print(f"{self.name} -> FAIL")

s1 = Student("Bhawna", 21, 85)
s2 = Student("Taman", 22, 28)

s1.result()    # Bhawna -> PASS
s2.result()    # Taman -> FAIL
```

---

## 4. Encapsulation
**Theory:** Bundling data (variables) and methods together inside a class and **restricting direct access** to internal data using access modifiers.

| Modifier | Syntax | Accessible From |
|---|---|---|
| Public | `self.name` | Anywhere |
| Protected | `self._name` | Class & subclasses |
| Private | `self.__name` | Only within class |

```python
class BankAccount:
    def __init__(self, owner, balance):
        self.owner = owner          # public
        self._branch = "Ludhiana"   # protected
        self.__balance = balance    # private

    def deposit(self, amount):
        self.__balance += amount
        print(f"Deposited {amount}. New Balance: {self.__balance}")

    def withdraw(self, amount):
        if amount > self.__balance:
            print("Insufficient balance!")
        else:
            self.__balance -= amount
            print(f"Withdrawn {amount}. New Balance: {self.__balance}")

    def get_balance(self):          # getter method
        return self.__balance

acc = BankAccount("Bhawna", 5000)
acc.deposit(2000)
acc.withdraw(1000)
print(acc.get_balance())            # 6000
# print(acc.__balance)  -> AttributeError (private, can't access directly)
```

---

## 5. Abstraction
**Theory:** Hiding **internal implementation** and showing only necessary functionality. Achieved using **Abstract Classes** via the `abc` module.

```python
from abc import ABC, abstractmethod

class Shape(ABC):                   # abstract class
    @abstractmethod
    def area(self):                 # abstract method – must be defined in child
        pass

    @abstractmethod
    def perimeter(self):
        pass

class Rectangle(Shape):
    def __init__(self, length, width):
        self.length = length
        self.width = width

    def area(self):
        return self.length * self.width

    def perimeter(self):
        return 2 * (self.length + self.width)

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return 3.14 * self.radius ** 2

    def perimeter(self):
        return 2 * 3.14 * self.radius

r = Rectangle(5, 3)
c = Circle(7)

print("Rectangle Area:", r.area())
print("Rectangle Perimeter:", r.perimeter())
print("Circle Area:", c.area())
print("Circle Perimeter:", c.perimeter())

# Shape()  -> TypeError: Can't instantiate abstract class
```

---

## 6. Inheritance
**Theory:** Child class acquires all properties and methods of the parent class.

### Single Inheritance (one parent → one child)
```python
class Animal:
    def __init__(self, name):
        self.name = name
    def eat(self):
        print(f"{self.name} is eating.")

class Dog(Animal):
    def bark(self):
        print(f"{self.name} is barking.")

d = Dog("Tommy")
d.eat()     # inherited
d.bark()    # own method
```

### Multilevel Inheritance (grandparent → parent → child)
```python
class Animal:
    def breathe(self):
        print("Breathing...")

class Dog(Animal):
    def bark(self):
        print("Barking...")

class Puppy(Dog):
    def weep(self):
        print("Weeping...")

p = Puppy()
p.breathe()   # from Animal
p.bark()      # from Dog
p.weep()      # own method
```

### Multiple Inheritance (two parents → one child)
```python
class Father:
    def coding(self):
        print("Father knows coding.")

class Mother:
    def cooking(self):
        print("Mother knows cooking.")

class Child(Father, Mother):
    def playing(self):
        print("Child loves playing.")

c = Child()
c.coding()    # from Father
c.cooking()   # from Mother
c.playing()   # own method
```

### Hierarchical Inheritance (one parent → many children)
```python
class Vehicle:
    def __init__(self, brand):
        self.brand = brand
    def start(self):
        print(f"{self.brand} is starting.")

class Car(Vehicle):
    def drive(self):
        print(f"{self.brand} is driving.")

class Bike(Vehicle):
    def ride(self):
        print(f"{self.brand} is riding.")

car = Car("Toyota")
bike = Bike("Honda")

car.start(); car.drive()
bike.start(); bike.ride()
```

### `super()` – Calling Parent Constructor
```python
class Animal:
    def __init__(self, name):
        self.name = name

class Dog(Animal):
    def __init__(self, name, breed):
        super().__init__(name)    # calling parent __init__
        self.breed = breed

    def display(self):
        print(f"Name: {self.name}, Breed: {self.breed}")

d = Dog("Tommy", "Labrador")
d.display()
```

---

## 7. Polymorphism
**Theory:** Same method name behaves differently depending on the object/class. Two types — Method Overriding and Duck Typing.

### Method Overriding
```python
class Animal:
    def sound(self):
        print("Animal makes a sound.")

class Dog(Animal):
    def sound(self):                    # override parent method
        print("Dog barks: Woof!")

class Cat(Animal):
    def sound(self):
        print("Cat meows: Meow!")

class Cow(Animal):
    def sound(self):
        print("Cow moos: Moo!")

animals = [Dog(), Cat(), Cow(), Animal()]
for animal in animals:
    animal.sound()                      # different behavior, same method name
```

### Duck Typing (Polymorphism without inheritance)
```python
class PDFReader:
    def open(self):
        print("Opening PDF file...")

class WordReader:
    def open(self):
        print("Opening Word file...")

class ExcelReader:
    def open(self):
        print("Opening Excel file...")

def open_file(reader):
    reader.open()                       # doesn't care about type, just method

open_file(PDFReader())
open_file(WordReader())
open_file(ExcelReader())
```

---

## 8. Dunder (Magic) Methods
**Theory:** Special methods surrounded by double underscores that Python calls automatically in certain situations.

```python
class Student:
    def __init__(self, name, marks):
        self.name = name
        self.marks = marks

    def __str__(self):                  # called when print(object)
        return f"Student({self.name}, {self.marks})"

    def __len__(self):                  # called when len(object)
        return self.marks

    def __add__(self, other):           # called when object1 + object2
        return self.marks + other.marks

    def __gt__(self, other):            # called when object1 > object2
        return self.marks > other.marks

s1 = Student("Bhawna", 85)
s2 = Student("Taman", 72)

print(s1)               # Student(Bhawna, 85)
print(len(s1))          # 85
print(s1 + s2)          # 157
print(s1 > s2)          # True
```

---

## 9. Quick Summary Table

| Concept | Keyword/Tool | Purpose |
|---|---|---|
| Class & Object | `class`, `object()` | Blueprint & instance |
| Constructor | `__init__`, `self` | Initialize attributes |
| Encapsulation | `_`, `__` | Access control |
| Abstraction | `ABC`, `@abstractmethod` | Hide implementation |
| Single Inheritance | `class Child(Parent)` | One parent |
| Multilevel | `A → B → C` | Chain of inheritance |
| Multiple | `class C(A, B)` | Two parents |
| Hierarchical | `A → B, A → C` | One parent, many children |
| Polymorphism | Method overriding | Same name, diff behavior |
| Magic Methods | `__str__`, `__add__` | Custom operator behavior |

---

## Summary of Day 9
Today I covered all major **OOP concepts** in Python — class/object creation, `__init__` with `self`, **encapsulation** (public/protected/private), **abstraction** (abstract classes using `ABC`), all **4 types of inheritance** (single, multilevel, multiple, hierarchical), **polymorphism** (method overriding and duck typing), and **dunder/magic methods** (`__str__`, `__add__`, `__gt__`, `__len__`). OOP makes code modular, reusable, and easy to maintain.

