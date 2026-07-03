# Daily Diary – Day 6
`date : 29/6/26 `
**Subject:** Python Programming
#### **Topic Covered:** Data Structures – Stack, Queue, Linked List, Tree (Binary Search Tree)

---

## 1. What are Data Structures? (Brief Theory)
Data structures are ways of **organizing and storing data** so it can be accessed and modified efficiently. Python supports built-in structures (list, dict, set, tuple) and also allows creating **user-defined structures** using classes.

| Data Structure | Type | Key Feature |
|---|---|---|
| Stack | Linear | Last In First Out (LIFO) |
| Queue | Linear | First In First Out (FIFO) |
| Linked List | Linear | Nodes connected via pointers |
| Tree | Non-Linear | Hierarchical parent-child structure |

---

## 2. Stack (LIFO – Last In First Out)
**Theory:** Like a stack of plates — the last item added is the first to be removed. Operations: `push` (add), `pop` (remove), `peek` (view top).

```python
class Stack:
    def __init__(self):
        self.stack = []

    def push(self, item):
        self.stack.append(item)
        print(f"{item} pushed to stack")

    def pop(self):
        if self.is_empty():
            return "Stack is empty!"
        return self.stack.pop()

    def peek(self):
        if self.is_empty():
            return "Stack is empty!"
        return self.stack[-1]

    def is_empty(self):
        return len(self.stack) == 0

    def display(self):
        print("Stack:", self.stack)

s = Stack()
s.push(10)
s.push(20)
s.push(30)
s.display()              # [10, 20, 30]
print(s.peek())          # 30
print(s.pop())           # 30
s.display()              # [10, 20]
```

---

## 3. Queue (FIFO – First In First Out)
**Theory:** Like a queue at a ticket counter — the first person to join is the first to leave. Operations: `enqueue` (add), `dequeue` (remove), `front` (view first).

```python
class Queue:
    def __init__(self):
        self.queue = []

    def enqueue(self, item):
        self.queue.append(item)
        print(f"{item} added to queue")

    def dequeue(self):
        if self.is_empty():
            return "Queue is empty!"
        return self.queue.pop(0)

    def front(self):
        if self.is_empty():
            return "Queue is empty!"
        return self.queue[0]

    def is_empty(self):
        return len(self.queue) == 0

    def display(self):
        print("Queue:", self.queue)

q = Queue()
q.enqueue("Ram")
q.enqueue("Sham")
q.enqueue("Gita")
q.display()              # ['Ram', 'Sham', 'Gita']
print(q.front())         # Ram
print(q.dequeue())       # Ram
q.display()              # ['Sham', 'Gita']
```

### Queue using Python's `deque` (Efficient Way)
```python
from collections import deque

dq = deque()
dq.append("Ram")         # enqueue
dq.append("Sham")
dq.append("Gita")
print(dq)
dq.popleft()             # dequeue (efficient O(1))
print(dq)
```

---

## 4. Linked List
**Theory:** A linked list is a series of **nodes** where each node stores **data** and a **pointer (next)** to the next node. Unlike lists, elements are not stored in contiguous memory.

```
[10 | next] --> [20 | next] --> [30 | None]
```

```python
# Node class
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

# Linked List class
class LinkedList:
    def __init__(self):
        self.head = None

    def insert_at_end(self, data):
        new_node = Node(data)
        if self.head is None:
            self.head = new_node
            return
        current = self.head
        while current.next:
            current = current.next
        current.next = new_node

    def insert_at_beginning(self, data):
        new_node = Node(data)
        new_node.next = self.head
        self.head = new_node

    def delete_node(self, data):
        if self.head is None:
            return
        if self.head.data == data:
            self.head = self.head.next
            return
        current = self.head
        while current.next:
            if current.next.data == data:
                current.next = current.next.next
                return
            current = current.next

    def display(self):
        current = self.head
        elements = []
        while current:
            elements.append(str(current.data))
            current = current.next
        print(" --> ".join(elements) + " --> None")

ll = LinkedList()
ll.insert_at_end(10)
ll.insert_at_end(20)
ll.insert_at_end(30)
ll.insert_at_beginning(5)
ll.display()              # 5 --> 10 --> 20 --> 30 --> None
ll.delete_node(20)
ll.display()              # 5 --> 10 --> 30 --> None
```

---

## 5. Binary Search Tree (BST)
**Theory:** A **tree** is a non-linear hierarchical structure. In a **Binary Search Tree**, each node has at most two children:
- **Left child** → smaller than parent
- **Right child** → greater than parent

```
        50
       /  \
      30   70
     / \   / \
    20  40 60  80
```

```python
class TreeNode:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

class BinarySearchTree:
    def __init__(self):
        self.root = None

    def insert(self, data):
        new_node = TreeNode(data)
        if self.root is None:
            self.root = new_node
            return
        current = self.root
        while True:
            if data < current.data:
                if current.left is None:
                    current.left = new_node
                    break
                current = current.left
            else:
                if current.right is None:
                    current.right = new_node
                    break
                current = current.right

    def inorder(self, node):
        if node:
            self.inorder(node.left)
            print(node.data, end=" ")
            self.inorder(node.right)

    def search(self, data):
        current = self.root
        while current:
            if data == current.data:
                return True
            elif data < current.data:
                current = current.left
            else:
                current = current.right
        return False

bst = BinarySearchTree()
bst.insert(50)
bst.insert(30)
bst.insert(70)
bst.insert(20)
bst.insert(40)
bst.insert(60)
bst.insert(80)

print("Inorder Traversal:")
bst.inorder(bst.root)      # 20 30 40 50 60 70 80

print("\nSearch 40:", bst.search(40))   # True
print("Search 99:", bst.search(99))    # False
```

---

## 6. Comparison – When to Use What?

| Structure | Use Case |
|---|---|
| Stack | Undo/Redo, browser back button, expression evaluation |
| Queue | Task scheduling, printer queue, customer service |
| Linked List | Frequent insertions/deletions, dynamic memory |
| BST | Fast searching, sorted data retrieval |

---

## Summary of Day 6
Today I learned about the four major data structures — **Stack** (LIFO using list/append/pop), **Queue** (FIFO using list/deque), **Linked List** (nodes connected via pointers, insert/delete operations), and **Binary Search Tree** (hierarchical structure with insert, search, and inorder traversal). Each was implemented from scratch using Python classes and `__init__`.

**Practice Questions for Tomorrow:**
1. Implement a stack and use it to reverse a string.
2. Use a queue to simulate a ticket booking system with 5 customers.
3. Create a linked list and write a function to count the total number of nodes.
4. Insert values `[15, 10, 20, 8, 12, 25]` into a BST and print inorder traversal.
5. Write a function to check if a stack is palindrome (without using reverse).