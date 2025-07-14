---
id: 14
date: 2025-07-14T00:00:00Z
title: Python Cheatsheet
author: Jeremy Novak
summary: Python programming language cheatsheet
slug: python-cheatsheet
tags:
  - python
published: true
---

# Python Cheatsheet

---

## Setup & Environment

- Install Python (macOS)
```bash
brew install python
```

- Install Python (Linux)
```bash
# Ubuntu/Debian
sudo apt update
sudo apt install python3 python3-pip

# CentOS/RHEL
sudo yum install python3 python3-pip
```

- Install Python (Windows)
1. Download from [python.org](https://www.python.org/downloads/)
2. Run installer and check "Add to PATH"
3. Or use Microsoft Store

- Check Python version
```bash
python --version
python3 --version
```

- Create virtual environment
```bash
python -m venv myenv
source myenv/bin/activate  # Linux/macOS
myenv\Scripts\activate     # Windows
```

- Deactivate virtual environment
```bash
deactivate
```

---

## Package Management

- Install package
```bash
pip install requests
```

- Install specific version
```bash
pip install requests==2.28.1
```

- Install from requirements file
```bash
pip install -r requirements.txt
```

- Generate requirements file
```bash
pip freeze > requirements.txt
```

- List installed packages
```bash
pip list
```

- Show package info
```bash
pip show requests
```

- Upgrade package
```bash
pip install --upgrade requests
```

- Uninstall package
```bash
pip uninstall requests
```

---

## Running Python

- Run Python file
```bash
python script.py
```

- Run Python interactively
```bash
python
```

- Run module as script
```bash
python -m http.server 8000
```

- Run with specific interpreter
```bash
python3.9 script.py
```

---

## Basic Python Structure

```python
#!/usr/bin/env python3

def main():
    print("Hello, World!")

if __name__ == "__main__":
    main()
```

---

## Variables and Data Types

- Numbers
```python
integer = 42
float_num = 3.14
complex_num = 1 + 2j
```

- Strings
```python
text = "Hello"
multiline = """This is a
multiline string"""
f_string = f"Hello {name}"
```

- Booleans
```python
is_true = True
is_false = False
```

- Lists
```python
numbers = [1, 2, 3, 4, 5]
mixed = [1, "hello", 3.14, True]
```

- Tuples
```python
coordinates = (10, 20)
single_item = (42,)
```

- Dictionaries
```python
person = {"name": "Alice", "age": 30}
empty_dict = {}
```

- Sets
```python
unique_numbers = {1, 2, 3, 4, 5}
empty_set = set()
```

---

## Control Flow

- If/elif/else
```python
if x > 0:
    print("Positive")
elif x < 0:
    print("Negative")
else:
    print("Zero")
```

- For loop
```python
for i in range(10):
    print(i)

for item in [1, 2, 3]:
    print(item)

for key, value in {"a": 1, "b": 2}.items():
    print(key, value)
```

- While loop
```python
i = 0
while i < 10:
    print(i)
    i += 1
```

- List comprehension
```python
squares = [x**2 for x in range(10)]
evens = [x for x in range(20) if x % 2 == 0]
```

- Match statement (Python 3.10+)
```python
match status:
    case "active":
        print("System is active")
    case "inactive":
        print("System is inactive")
    case _:
        print("Unknown status")
```

---

## Functions

- Define function
```python
def greet(name, greeting="Hello"):
    return f"{greeting}, {name}!"

def add_numbers(*args):
    return sum(args)

def create_person(**kwargs):
    return kwargs
```

- Lambda functions
```python
square = lambda x: x**2
add = lambda x, y: x + y
```

- Decorators
```python
def my_decorator(func):
    def wrapper(*args, **kwargs):
        print("Before function call")
        result = func(*args, **kwargs)
        print("After function call")
        return result
    return wrapper

@my_decorator
def say_hello():
    print("Hello!")
```

---

## Classes and Objects

- Define class
```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def greet(self):
        return f"Hello, I'm {self.name}"
    
    def __str__(self):
        return f"Person(name='{self.name}', age={self.age})"
```

- Inheritance
```python
class Student(Person):
    def __init__(self, name, age, student_id):
        super().__init__(name, age)
        self.student_id = student_id
    
    def study(self):
        return f"{self.name} is studying"
```

- Properties
```python
class Circle:
    def __init__(self, radius):
        self._radius = radius
    
    @property
    def radius(self):
        return self._radius
    
    @radius.setter
    def radius(self, value):
        if value < 0:
            raise ValueError("Radius cannot be negative")
        self._radius = value
    
    @property
    def area(self):
        return 3.14159 * self._radius ** 2
```

---

## Exception Handling

- Try/except/finally
```python
try:
    result = 10 / 0
except ZeroDivisionError as e:
    print(f"Error: {e}")
except Exception as e:
    print(f"Unexpected error: {e}")
finally:
    print("This always executes")
```

- Raise exceptions
```python
def check_age(age):
    if age < 0:
        raise ValueError("Age cannot be negative")
    return age

def custom_exception():
    raise Exception("Something went wrong")
```

- Custom exceptions
```python
class CustomError(Exception):
    def __init__(self, message):
        self.message = message
        super().__init__(self.message)

raise CustomError("This is a custom error")
```

---

## File I/O

- Read file
```python
with open("file.txt", "r") as f:
    content = f.read()

with open("file.txt", "r") as f:
    lines = f.readlines()

with open("file.txt", "r") as f:
    for line in f:
        print(line.strip())
```

- Write file
```python
with open("output.txt", "w") as f:
    f.write("Hello, World!")

with open("output.txt", "a") as f:
    f.write("Appended text")
```

- JSON files
```python
import json

# Write JSON
data = {"name": "Alice", "age": 30}
with open("data.json", "w") as f:
    json.dump(data, f)

# Read JSON
with open("data.json", "r") as f:
    data = json.load(f)
```

---

## Common Built-in Functions

- Type and conversion
```python
type(42)           # <class 'int'>
int("42")          # 42
float("3.14")      # 3.14
str(42)            # "42"
bool(1)            # True
```

- Math functions
```python
abs(-5)            # 5
round(3.14159, 2)  # 3.14
min(1, 2, 3)       # 1
max(1, 2, 3)       # 3
sum([1, 2, 3])     # 6
```

- Sequence functions
```python
len([1, 2, 3])     # 3
sorted([3, 1, 2])  # [1, 2, 3]
reversed([1, 2, 3]) # [3, 2, 1]
enumerate(["a", "b", "c"])  # [(0, 'a'), (1, 'b'), (2, 'c')]
zip([1, 2, 3], ["a", "b", "c"])  # [(1, 'a'), (2, 'b'), (3, 'c')]
```

- Filter and map
```python
list(filter(lambda x: x > 0, [-1, 0, 1, 2]))  # [1, 2]
list(map(lambda x: x**2, [1, 2, 3, 4]))       # [1, 4, 9, 16]
```

---

## String Methods

```python
text = "Hello World"
text.upper()           # "HELLO WORLD"
text.lower()           # "hello world"
text.strip()           # Remove whitespace
text.replace("World", "Python")  # "Hello Python"
text.split()           # ["Hello", "World"]
text.startswith("Hello")  # True
text.endswith("World")    # True
text.find("World")        # 6
"Python" in text          # False
```

---

## List Methods

```python
numbers = [1, 2, 3]
numbers.append(4)      # [1, 2, 3, 4]
numbers.insert(0, 0)   # [0, 1, 2, 3, 4]
numbers.remove(2)      # [0, 1, 3, 4]
numbers.pop()          # Returns and removes last item
numbers.sort()         # Sort in place
numbers.reverse()      # Reverse in place
numbers.count(1)       # Count occurrences
numbers.index(3)       # Find index of item
```

---

## Dictionary Methods

```python
person = {"name": "Alice", "age": 30}
person.keys()          # dict_keys(['name', 'age'])
person.values()        # dict_values(['Alice', 30])
person.items()         # dict_items([('name', 'Alice'), ('age', 30)])
person.get("name")     # "Alice"
person.get("email", "N/A")  # "N/A" (default value)
person.update({"city": "New York"})  # Add/update items
person.pop("age")      # Remove and return value
```

---

## Modules and Imports

- Import module
```python
import math
import os
from datetime import datetime
from collections import Counter
import json as js
```

- Create module (save as mymodule.py)
```python
def greet(name):
    return f"Hello, {name}!"

PI = 3.14159
```

- Use module
```python
import mymodule
print(mymodule.greet("Alice"))
print(mymodule.PI)
```

---

## Common Standard Library Modules

- datetime
```python
from datetime import datetime, timedelta

now = datetime.now()
tomorrow = now + timedelta(days=1)
formatted = now.strftime("%Y-%m-%d %H:%M:%S")
```

- os and pathlib
```python
import os
from pathlib import Path

os.getcwd()            # Current directory
os.listdir(".")        # List files
os.path.exists("file.txt")  # Check if file exists

path = Path("folder/file.txt")
path.parent            # folder
path.name              # file.txt
path.suffix            # .txt
```

- random
```python
import random

random.randint(1, 10)  # Random integer
random.choice([1, 2, 3, 4, 5])  # Random choice
random.shuffle([1, 2, 3, 4, 5])  # Shuffle list
```

- collections
```python
from collections import Counter, defaultdict

counter = Counter([1, 2, 2, 3, 3, 3])
# Counter({3: 3, 2: 2, 1: 1})

dd = defaultdict(list)
dd["key"].append("value")
```

---

## Virtual Environment Best Practices

- Create project-specific environment
```bash
python -m venv project_env
source project_env/bin/activate
```

- Install packages for project
```bash
pip install requests flask
pip freeze > requirements.txt
```

- Recreate environment
```bash
pip install -r requirements.txt
```

---

## Testing

- Simple test with assert
```python
def test_add():
    assert add(2, 3) == 5
    assert add(-1, 1) == 0
```

- unittest module
```python
import unittest

class TestMath(unittest.TestCase):
    def test_add(self):
        self.assertEqual(add(2, 3), 5)
    
    def test_subtract(self):
        self.assertEqual(subtract(5, 3), 2)

if __name__ == "__main__":
    unittest.main()
```

- pytest (install with pip install pytest)
```python
def test_add():
    assert add(2, 3) == 5

def test_subtract():
    assert subtract(5, 3) == 2
```

---

## Common Patterns

- Context managers
```python
class MyContext:
    def __enter__(self):
        print("Entering context")
        return self
    
    def __exit__(self, exc_type, exc_val, exc_tb):
        print("Exiting context")

with MyContext() as ctx:
    print("Inside context")
```

- Generators
```python
def count_up_to(n):
    count = 1
    while count <= n:
        yield count
        count += 1

for num in count_up_to(5):
    print(num)
```

- Iterator protocol
```python
class Counter:
    def __init__(self, max_count):
        self.max_count = max_count
        self.count = 0
    
    def __iter__(self):
        return self
    
    def __next__(self):
        if self.count < self.max_count:
            self.count += 1
            return self.count
        raise StopIteration
```

---

## Useful Third-Party Packages

- requests — HTTP library
```bash
pip install requests
```

- pandas — Data manipulation
```bash
pip install pandas
```

- numpy — Numerical computing
```bash
pip install numpy
```

- flask — Web framework
```bash
pip install flask
```

- pytest — Testing framework
```bash
pip install pytest
```

---

## Resources

- [Python.org](https://www.python.org/)
- [Python Documentation](https://docs.python.org/)
- [Real Python](https://realpython.com/)
- [Python Package Index (PyPI)](https://pypi.org/)
- [PEP 8 Style Guide](https://www.python.org/dev/peps/pep-0008/)
