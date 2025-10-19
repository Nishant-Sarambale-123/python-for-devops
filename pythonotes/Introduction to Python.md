Absolutely ✅
Here are **detailed, structured, and interview-ready notes** on **Python Fundamentals (Core Concepts)** — perfect for DevOps or Python preparation.

---

## 🐍 **1. Introduction to Python**

### What is Python?

* Python is a **high-level**, **interpreted**, **object-oriented**, and **general-purpose** programming language.
* It emphasizes **readability** and **simplicity** — “**less code, more power**”.

### Features:

* Easy to learn and write.
* Open-source and cross-platform.
* Huge standard library.
* Dynamically typed (no need to declare variable types).
* Supports multiple paradigms (OOP, procedural, functional).

### Installation:

* Download from [python.org](https://www.python.org/downloads/)
* Verify version:

  ```bash
  python --version
  ```
* Interactive shell:

  ```bash
  python
  ```

### Common IDEs:

* VS Code
* PyCharm
* Jupyter Notebook

---

## 🧮 **2. Variables and Data Types**

### Variables

* Containers to store data values.
* Created automatically when assigned a value.

```python
x = 10
name = "Nishant"
pi = 3.14
```

No need to declare types — Python is **dynamically typed**.

### Rules:

* Must start with a letter or underscore.
* Case-sensitive.
* No spaces or special characters.

---

### Built-in Data Types:

| Type    | Example                        | Description              |
| ------- | ------------------------------ | ------------------------ |
| `int`   | 10, -5                         | Integer numbers          |
| `float` | 3.14                           | Decimal numbers          |
| `str`   | "Hello"                        | Text/string              |
| `bool`  | True, False                    | Boolean values           |
| `list`  | [1, 2, 3]                      | Ordered, mutable         |
| `tuple` | (1, 2, 3)                      | Ordered, immutable       |
| `set`   | {1, 2, 3}                      | Unordered, unique values |
| `dict`  | {"name": "Nishant", "age": 25} | Key-value pairs          |

---

## 🔄 **3. Type Casting & Input/Output**

### Type Casting:

Convert one type to another using built-in functions:

```python
x = int("10")
y = float(5)
z = str(100)
```

### Input / Output:

```python
name = input("Enter your name: ")
print("Hello", name)
```

* `input()` always returns string type.
* Use type casting to convert:

  ```python
  age = int(input("Enter age: "))
  ```

---

## ➕ **4. Operators**

| Type       | Example                             | Description              |
| ---------- | ----------------------------------- | ------------------------ |
| Arithmetic | `+`, `-`, `*`, `/`, `%`, `//`, `**` | Basic math operations    |
| Comparison | `==`, `!=`, `>`, `<`, `>=`, `<=`    | Compare values           |
| Logical    | `and`, `or`, `not`                  | Combine conditions       |
| Assignment | `=`, `+=`, `-=`, `*=`, `/=`         | Assign and update values |
| Membership | `in`, `not in`                      | Check if element exists  |
| Identity   | `is`, `is not`                      | Compare memory locations |

**Example:**

```python
x, y = 10, 20
print(x > y and y > 5)  # False
```

---

## ⚙️ **5. Conditional Statements**

Used to make decisions in code.

```python
age = 20
if age >= 18:
    print("Adult")
elif age > 13:
    print("Teen")
else:
    print("Child")
```

🧠 **Tip:** Indentation defines code blocks in Python (usually 4 spaces).

---

## 🔁 **6. Loops**

### For Loop

Used to iterate over a sequence.

```python
for i in range(5):
    print(i)
```

### While Loop

Runs until a condition becomes False.

```python
count = 0
while count < 5:
    print(count)
    count += 1
```

### Control Statements

* `break`: exit loop
* `continue`: skip current iteration
* `pass`: do nothing (placeholder)

---

## 🧩 **7. Functions**

Reusable blocks of code.

### Define & Call:

```python
def greet(name):
    return f"Hello {name}"

print(greet("Nishant"))
```

### Default Arguments:

```python
def add(a, b=10):
    return a + b
```

### Variable Arguments:

```python
def show(*args, **kwargs):
    print(args)      # Tuple
    print(kwargs)    # Dictionary
```

Example:

```python
show(1, 2, 3, name="Nishant", age=25)
```

---

## 🚨 **8. Exception Handling**

Used to handle runtime errors gracefully.

```python
try:
    x = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero!")
finally:
    print("Done!")
```

**Common Exceptions:**

* `ZeroDivisionError`
* `FileNotFoundError`
* `ValueError`
* `TypeError`
* `KeyError`

---

## 📂 **9. File Handling**

Used for reading and writing files.

### Open File:

```python
f = open("data.txt", "r")
```

Modes:

* `"r"` → read
* `"w"` → write (overwrite)
* `"a"` → append
* `"r+"` → read & write

### Read:

```python
content = f.read()
print(content)
f.close()
```

### Write:

```python
f = open("data.txt", "w")
f.write("Hello World")
f.close()
```

### With Context Manager (recommended):

Automatically closes the file.

```python
with open("data.txt", "r") as f:
    data = f.read()
```

---

## 📦 **10. Modules and Packages**

### Module:

A Python file (`.py`) containing code — variables, functions, classes.

```python
# mymodule.py
def greet(name):
    return f"Hello {name}"
```

Use:

```python
import mymodule
print(mymodule.greet("Nishant"))
```

### Built-in Modules:

```python
import math, os, sys, random
print(math.sqrt(16))
```

### Packages:

A folder containing multiple modules + `__init__.py` file.

Example structure:

```
mypackage/
    __init__.py
    module1.py
    module2.py
```

Import:

```python
from mypackage import module1
```

---

## ✅ **Summary Table**

| Concept       | Purpose              | Example               |
| ------------- | -------------------- | --------------------- |
| Variables     | Store data           | `x = 10`              |
| Data Types    | Define type of value | `str`, `list`, `dict` |
| Operators     | Perform operations   | `x + y`               |
| Conditionals  | Decision making      | `if…else`             |
| Loops         | Repeat code          | `for`, `while`        |
| Functions     | Reusable code        | `def add(a,b)`        |
| Exceptions    | Handle errors        | `try-except`          |
| File Handling | Read/write files     | `open("file")`        |
| Modules       | Reuse code           | `import os`           |

---

Would you like me to create a **separate “DevOps-focused Python version”** of these notes next — focusing on automation, AWS, file ops, subprocess, OS, JSON, and Boto3 usage?
That would connect this foundation to real DevOps scripting.
