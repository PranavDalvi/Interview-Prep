## Python
1. **What is inheritance and polymorphism in python**
	- One class derives properties and methods from another is called as inheritance like child inherit its parent.
	- Same method name, different behaviour is known as polymorphism.
		- **Interview note:** Python supports **duck typing**, so polymorphism doesn’t require inheritance.
***
### Reference & Mutability

This document contains **common Python interview traps** related to **references, mutability, and copying**, written in **Q&A format** for quick revision.

---
### Add ONE real backend example per concept
Example:
- **Dict** → request payload / user data
- **Set** → removing duplicate user IDs
- **Tuple** → fixed DB query parameters
- **Immutable types** → safer function arguments
Prepare **1 sentence per concept**.

## Q1. What will be the output of the following code?

```python
a = [1, 2, 3]
b = a
b.append(4)
print(a)
```

### ✅ Answer:

```text
[1, 2, 3, 4]
```

### 🧠 Explanation:

In Python, assignment does **not create a copy** of a mutable object. Both `a` and `b` point to the **same list in memory**. Modifying the list via `b` also affects `a`.

**Key line to remember:**

> Assignment copies the reference, not the object.

---

## Q2. How can you modify `b` without affecting `a`?

```python
a = [1, 2, 3]
b = a
```

### ✅ Answer (any one):

```python
b = a[:]        # slicing copy
# OR
b = a.copy()    # shallow copy
# OR
b = list(a)     # constructor copy
```

### 🧠 Explanation:

These methods create a **new list object** in memory. Changes to `b` will not affect `a`.

---

## Q3. What will be the output here?

```python
a = [1, 2, 3]
b = a[:]
b.append(4)
print(a)
```

### ✅ Answer:

```text
[1, 2, 3]
```

### 🧠 Explanation:

Slicing (`a[:]`) creates a **new list**, so `b` is independent of `a`.

---

## Q4. What is the output of this code?

```python
a = 10
b = a
b = 20
print(a)
```

### ✅ Answer:

```text
10
```

### 🧠 Explanation:

Integers are **immutable**. Reassigning `b` creates a new object and does not affect `a`.

---

## Q5. What will this print?

```python
a = [1, 2]
b = a
a.append(3)
print(b)
```

### ✅ Answer:

```text
[1, 2, 3]
```

### 🧠 Explanation:

Both `a` and `b` refer to the **same mutable list**, so changes via either variable affect the same object.

---

## Q6. Why does this behavior matter in backend applications?

### ✅ Answer:

In backend systems, shared mutable objects can cause:
- Unexpected side effects
- Hard-to-debug bugs
- Data corruption in shared state

Using copies or immutable objects helps ensure **predictability and safety**, especially in APIs, services, and concurrent code.

---

## ✅ One-line Summary (Interview Gold)

> **Mutable objects share changes when assigned; immutable objects do not.**

---

## ✅ Interview Tip

If you ever get confused, say:

> "I need to check whether the object is mutable and whether this is a reference or a copy."

Interviewers appreciate correct reasoning more than speed.

# Tuple vs List

## Q1. Why is a tuple faster than a list?

### ✅ Answer:

Tuples are faster than lists because they are **immutable**. Since their size and contents cannot change, Python can optimize memory allocation and access for tuples.

### 🧠 Explanation:

- Tuples have a **fixed structure**, so Python does not need to manage dynamic resizing.
- Less memory overhead compared to lists.
- Faster iteration and access in many cases.

**Interview-safe one-liner:**

> "Tuples are faster because they are immutable and require less overhead than lists."

---

## Q2. Why would you use a tuple over a list?

### ✅ Answer:

Tuples are used when the data is **fixed and should not change**.

A list is a mutable data structure, so it can be modified after creation, whereas a tuple is immutable and cannot be changed once defined. Lists are used when data needs to be updated, such as counters or collections that change over time. Tuples are used when data should remain fixed, like configuration values or database query parameters, because immutability makes them safer.
### 🧠 Common Use Cases:

- Configuration values
- Coordinates (x, y)    
- Database records
- Function return values with multiple items

### 🔐 Benefits:

- Prevents accidental modification
- Makes code safer and more predictable
- Can be used as dictionary keys (lists cannot)

**Interview-safe answer:**

> "I use tuples when data should remain constant and should not be modified accidentally."

---

## Q3. What happens if you modify a list inside a function?

### Example:
```python
def add_item(lst):
lst.append(4)

nums = [1, 2, 3]

add_item(nums)
print(nums)
```
### ✅ Output:
```python
[1, 2, 3, 4]
```
### 🧠 Explanation:
Lists are **mutable**. When a list is passed to a function, the function receives a **reference** to the same list object. Any modification inside the function affects the original list.

**Interview-safe explanation:**
> "Since lists are mutable, changes made inside a function affect the original list unless a copy is passed."

---
## Q4. Why is immutability useful?

### ✅ Answer:
Immutability helps make programs **safer, predictable, and easier to debug**.
### 🧠 Key Benefits:
- Prevents accidental data modification
- Makes code easier to reason about
- Reduces side effects
- Useful in concurrent and multi-threaded environments

### 📌 Backend Context:
- Prevents shared-state bugs
- Safer function arguments
- Better reliability in APIs and services

**Interview one-liner:**
> "Immutability prevents unintended side effects and makes backend systems more reliable."

---
## ✅ Quick Summary (Revise Before Interview)
- Tuples are faster because they are immutable    
- Use tuples when data should not change
- Modifying a list inside a function affects the original list
- Immutability improves safety and predictability
***
# Exception Handling

## Q1. What is the difference between parameters and arguments?

### ✅ Answer:
**Parameters** are the variables defined in a function definition, while **arguments** are the actual values passed to the function when it is called.
### Example:
```python
def add(a, b):   # a and b are parameters
    return a + b

add(2, 3)        # 2 and 3 are arguments
```
### 🧠 Explanation:
- Parameters act as placeholders
- Arguments supply real data at runtime

**Interview one-liner:**
> "Parameters are defined in the function signature, arguments are the values passed during the function call."

---
## Q2. Can a `finally` block update or override a return value?
### ✅ Answer:
Yes. If a `return` statement is present inside the `finally` block, it **overrides any return value** from the `try` or `except` blocks.
### Example:
```python
def test():
    try:
        return 1
    finally:
        return 2

print(test())
```
### ✅ Output:
```text
2
```
### 🧠 Explanation:
- The `finally` block **always executes**
- A return inside `finally` replaces earlier returns
⚠️ This is considered **bad practice** because it hides exceptions and return values.

**Interview-safe answer:**
> "Yes, a return in finally overrides previous returns, but it should generally be avoided."

---
## Q3. What is the purpose of the `finally` block?
### ✅ Answer:
The `finally` block is used to execute **cleanup code** that must run regardless of whether an exception occurs.
### Common Use Cases:
- Closing database connections
- Releasing file handles
- Cleaning up resources

**Interview one-liner:**
> "Finally is used for cleanup logic that must execute even if an exception occurs."

---
## Q4. What happens if an exception occurs and there is no `except` block?
### ✅ Answer:
The `finally` block will still execute, and then the exception will propagate upward.
### Example:

```python
def demo():
    try:
        x = 1 / 0
    finally:
        print("Cleanup")

demo()
```
### ✅ Output:
```bash
Cleanup
ERROR!
Traceback (most recent call last):
ZeroDivisionError: division by zero
```
### 🧠 Explanation:
- `finally` runs first
- Exception is raised after

---
# Function Arguments

## Q1. What are default arguments in Python?

### ✅ Answer:
Default arguments are parameters that assume a **default value** if no argument is provided during the function call.
### Example:

```python
def greet(name="User"):
    return f"Hello {name}"

print(greet())        # Hello User
print(greet("Amit")) # Hello Amit
```
### 🧠 Explanation:
- Default values are assigned **at function definition time**
- They make functions flexible and easier to call

**Interview one‑liner:**

> "Default arguments provide fallback values when arguments are not passed."

---
## Q2. What is the difference between positional and keyword arguments?

### ✅ Answer:

- **Positional arguments** are passed based on position
- **Keyword arguments** are passed using parameter names
### Example:

```python
def add(a, b):
    return a + b

add(2, 3)        # positional
add(a=2, b=3)    # keyword
```
### 🧠 Explanation:
- Positional arguments must follow order
- Keyword arguments improve readability and flexibility

**Interview‑safe answer:**

> "Positional arguments depend on order, keyword arguments depend on parameter names."

---
## Q3. What are `*args` and `**kwargs`? (Conceptual)

### ✅ Answer:
- `*args` allows passing a **variable number of positional arguments**
- `**kwargs` allows passing a **variable number of keyword arguments**
### Example:

```python
def demo(*args, **kwargs):
    print(args)
    print(kwargs)

demo(1, 2, 3, name="Pranav", role="Backend")
```
### ✅ Output:
```python
(1, 2, 3)
{'name': 'Pranav', 'role': 'Backend'}
```
### 🧠 Explanation:
- `args` is a tuple
- `kwargs` is a dictionary

**Interview one‑liner:**

> "`*args` handles variable positional arguments, `**kwargs` handles variable keyword arguments."

---

## Q4. What is the mutable default argument trap? (VERY IMPORTANT)

### ❌ Problematic Code:

```python
def add_item(item, items=[]):
    items.append(item)
    return items

print(add_item(1))
print(add_item(2))
```

### Output:

```text
[1]
[1, 2]
```

### 🧠 Why this happens:

- Default arguments are evaluated **only once**
- The same list is reused across function calls

This leads to **unexpected shared state**.

---

## ✅ Correct Way to Handle Defaults

### ✔ Safe Pattern:

```python
def add_item(item, items=None):
    if items is None:
        items = []
    items.append(item)
    return items
    
print(add_item(1))
print(add_item(2))
```

### ✔ Output:

```text
[1]
[2]
```

### 🧠 Explanation:
- `None` is immutable
- A new list is created per call

**Interview‑safe answer:**

> "Mutable objects should never be used as default arguments because they persist across calls."

---

## ✅ Quick Summary (Must Remember)

- Default arguments are evaluated once
- Positional arguments depend on order
- Keyword arguments improve clarity
- `*args` → tuple of extra positional args
- `**kwargs` → dict of extra keyword args
- Mutable defaults cause shared‑state bugs
---
## Q5. When should you use `*args` and when should you use `**kwargs`?

### ✅ Answer:

- Use `*args` when you want to accept a **variable number of positional arguments** and the order of values matters.
- Use `**kwargs` when you want to accept a **variable number of keyword arguments** and you need named, flexible parameters.
### 🧠 Practical Examples:

#### Using `*args`

```python
def total_sum(*args):
    return sum(args)

# Usage
total_sum(1, 2, 3, 4)
```
### ✅ Output:
```python
10
```

Use `*args` when:
- Number of inputs is unknown
- Values are similar in meaning
- Order is important
---
#### Using `**kwargs`

```python
def create_user(**kwargs):
    return kwargs

# Usage
create_user(name="Pranav", role="Backend", exp=2)
```
Use `**kwargs` when:
- You need flexibility in named parameters
- Passing optional or configuration data
- Building APIs or framework-level functions
### ⚠️ Important Note:
- `*args` collects arguments into a **tuple**
- `**kwargs` collects arguments into a **dictionary**

**Interview one-liner:**

> "Use `*args` for variable positional values and `**kwargs` for flexible named parameters."

***
# OOP 

## Q1. What is Object-Oriented Programming (OOP)?

### ✅ Answer:

Object-Oriented Programming is a programming paradigm that organizes code into **objects**, which contain **data (attributes)** and **behavior (methods)**.
### 🧠 Explanation:

OOP helps in:
- Structuring large applications
- Improving code reusability
- Making systems easier to maintain

**Interview one-liner:**

> "OOP helps structure code using objects that bundle data and behavior together."

---

## Q2. What is a class and an object?

### ✅ Answer:

- A **class** is a blueprint or template
- An **object** is an instance of a class

### Example:

```python
class User:
    def __init__(self, name):
        self.name = name

u = User("Pranav")  # object
```

**Interview-safe explanation:**

> "A class defines structure and behavior, while an object represents a real instance of that class."

---

## Q3. What are the four pillars of OOP?

### ✅ Answer:

1. Encapsulation
2. Inheritance
3. Polymorphism
4. Abstraction

---

## Q4. What is Encapsulation?
### ✅ Answer:
Encapsulation is the practice of **bundling data and methods together** and **restricting direct access** to internal data.
### Example:
```python
class Account:
    def __init__(self):
        self._balance = 0
```
### 🧠 Explanation:
- `_balance` indicates internal usage
- Prevents accidental misuse

**Interview one-liner:**
> "Encapsulation hides internal state and exposes only required behavior."

---
## Q5. What is Inheritance?
### ✅ Answer:
Inheritance allows a class to **reuse properties and methods** of another class.
### Example:
```python
class BaseService:
    def log(self):
        print("Logging")

class UserService(BaseService):
    pass
```
### 🧠 Explanation:
- Promotes code reuse
- Supports hierarchical design

**Interview one-liner:**
> "Inheritance allows child classes to reuse and extend parent class functionality."

---
## Q6. What is Polymorphism?
### ✅ Answer:
Polymorphism allows the **same method name** to behave differently depending on the object.
### Example:

```python
class Animal:
    def speak(self):
        pass

class Dog(Animal):
    def speak(self):
        return "Bark"
```

### 🧠 Explanation:
- Method overriding is a common form
- Enables flexible design

**Interview one-liner:**

> "Polymorphism allows the same interface to have different implementations."

---
## Q7. What is Abstraction?
### ✅ Answer:
Abstraction focuses on **what an object does**, not **how it does it**.
### Example (conceptual):
```python
from abc import ABC, abstractmethod

class Payment(ABC):
    @abstractmethod
    def pay(self):
        pass
```

### 🧠 Explanation:
- Hides implementation details
- Exposes only essential functionality

**Interview one-liner:**
> "Abstraction exposes only essential behavior while hiding implementation details."

---
## Q8. What is method overriding?
### ✅ Answer:
Method overriding occurs when a child class provides its **own implementation** of a parent class method.
### Example:
```python
class Parent:
    def show(self):
        print("Parent")

class Child(Parent):
    def show(self):
        print("Child")
```

**Interview-safe answer:**
> "Method overriding allows child classes to customize parent behavior."
---
## Q9. Where have you used OOP concepts in backend systems?
### ✅ Sample Answer:
> "In backend systems, I use OOP to structure services. For example, base service classes handle shared logic like logging and validation, while child services implement business-specific behavior. This improves reuse and maintainability."

---
## Q10. Why is OOP important in backend development?
### ✅ Answer:

OOP helps backend systems by:
- Organizing complex logic
- Reducing code duplication
- Improving readability and testability
- Supporting scalable architecture

**Interview one-liner:**

> "OOP makes backend systems modular, maintainable, and easier to scale."

---

## ✅ Quick Revision Summary
- Class = blueprint, Object = instance
- Encapsulation protects internal state
- Inheritance enables reuse
- Polymorphism enables flexibility
- Abstraction hides complexity

---