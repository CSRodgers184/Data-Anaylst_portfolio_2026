# Python Reference

Practical quick-reference for data analysis and Domain Specialist work. Focused on what you actually use in notebooks, scripts, and portfolio projects.

---

## 1. Basics

### Input / Output

```python
# Output
print("Hello")
print("Age:", 25)
print(f"Name: {name}, Age: {age}")          # f-string (preferred)

# Input (always returns string)
name = input("Enter name: ")
age = int(input("Enter age: "))              # convert to int
```

### Variables

```python
x = 10
name = "Chris"
is_active = True

# Multiple assignment
a, b, c = 1, 2, 3
x = y = z = 0
```

### Operators

**Arithmetic**
```python
+  -  *  /  //  %  **          # // floor division, ** power
```

**Comparison**
```python
==  !=  >  <  >=  <=
```

**Logical**
```python
and  or  not
```

**Assignment**
```python
=  +=  -=  *=  /=  //=  %=
```

**Membership / Identity**
```python
in  not in
is  is not
```

### Keywords (common)

```python
False  True  None
and  or  not
if  elif  else
for  while  break  continue  pass
def  return  lambda
class  self
try  except  finally  raise
import  from  as
in  is  del  global  nonlocal
with  yield  async  await
```

### Data Types

| Type      | Example              | Mutable? |
|-----------|----------------------|----------|
| int       | `42`                 | No       |
| float     | `3.14`               | No       |
| str       | `"text"`             | No       |
| bool      | `True` / `False`     | No       |
| list      | `[1, 2, 3]`          | Yes      |
| tuple     | `(1, 2, 3)`          | No       |
| dict      | `{"a": 1}`           | Yes      |
| set       | `{1, 2, 3}`          | Yes      |
| NoneType  | `None`               | No       |

```python
type(x)          # check type
int("10")        # convert
str(42)
float("3.14")
bool(1)          # True
```

### Conditional Statements

```python
if age >= 18:
    print("Adult")
elif age >= 13:
    print("Teen")
else:
    print("Child")

# Ternary
status = "Adult" if age >= 18 else "Minor"
```

### Loops

```python
# for loop
for i in range(5):               # 0 to 4
    print(i)

for item in my_list:
    print(item)

for i, val in enumerate(my_list):
    print(i, val)

# while loop
count = 0
while count < 5:
    print(count)
    count += 1

# Control
break       # exit loop
continue    # skip to next iteration
pass        # do nothing (placeholder)
```

### Functions

```python
def greet(name, greeting="Hello"):
    return f"{greeting}, {name}"

# Lambda (anonymous)
square = lambda x: x ** 2

# *args and **kwargs
def func(*args, **kwargs):
    print(args)      # tuple
    print(kwargs)    # dict
```

---

## 2. Data Structures

### String

```python
s = "Glorystone Analytics"

s.lower()  /  s.upper()  /  s.title()
s.strip()  /  s.lstrip()  /  s.rstrip()
s.replace("old", "new")
s.split(",")                     # list
",".join(list_of_strings)
s.startswith("G")  /  s.endswith("s")
s.find("stone")                  # index or -1
len(s)
s[0]  /  s[-1]  /  s[0:5]        # slicing
```

### List

```python
lst = [1, 2, 3, "a"]

lst.append(4)
lst.extend([5, 6])
lst.insert(0, 0)
lst.remove(3)                    # by value
lst.pop()                        # last item
lst.pop(0)                       # by index
del lst[1]
lst.sort()  /  sorted(lst)
lst.reverse()
len(lst)
2 in lst

# List comprehension (powerful)
squares = [x**2 for x in range(10) if x % 2 == 0]
```

### Tuple

Immutable sequence.

```python
t = (1, 2, 3)
t = 1, 2, 3                      # parentheses optional

t[0]
len(t)
t.count(2)
t.index(3)

# Unpacking
a, b, c = t
```

### Dictionary

```python
d = {"name": "Chris", "role": "Domain Specialist"}

d["name"]
d.get("age", 0)                  # safe access with default
d["city"] = "Flower Mound"
d.update({"age": 35})
d.keys()  /  d.values()  /  d.items()
d.pop("role")
"name" in d

# Dict comprehension
{x: x**2 for x in range(5)}
```

### Set

Unordered, unique elements. Fast membership testing.

```python
s = {1, 2, 3, 3}                 # {1, 2, 3}

s.add(4)
s.remove(2)                      # error if missing
s.discard(2)                     # safe
s.union(other)
s.intersection(other)
s.difference(other)
```

---

## 3. Advanced Python

### OOP Concepts

```python
class Analyst:
    def __init__(self, name, specialty):
        self.name = name
        self.specialty = specialty

    def introduce(self):
        return f"{self.name} - {self.specialty}"

# Inheritance
class DomainSpecialist(Analyst):
    def __init__(self, name, domain):
        super().__init__(name, "Domain Specialist")
        self.domain = domain

# Key ideas
# - Encapsulation: data + methods in one unit
# - Inheritance: reuse and extend
# - Polymorphism: same interface, different behavior
# - Abstraction: hide complexity
```

### Exception Handling

```python
try:
    result = 10 / 0
except ZeroDivisionError as e:
    print("Cannot divide by zero:", e)
except Exception as e:
    print("Something went wrong:", e)
else:
    print("No error occurred")
finally:
    print("Always runs")

# Raise your own
if age < 0:
    raise ValueError("Age cannot be negative")
```

### File Handling

```python
# Read
with open("data.csv", "r") as f:
    content = f.read()
    # or
    lines = f.readlines()

# Write
with open("output.txt", "w") as f:
    f.write("Hello\n")

# Append
with open("log.txt", "a") as f:
    f.write("New line\n")

# Common modes: "r", "w", "a", "rb", "wb"
```

### Working with Databases

**MySQL (via mysql-connector or SQLAlchemy)**
```python
import mysql.connector

conn = mysql.connector.connect(
    host="localhost",
    user="root",
    password="password",
    database="glorystone"
)
cursor = conn.cursor()
cursor.execute("SELECT * FROM orders LIMIT 10")
rows = cursor.fetchall()
conn.close()
```

**MongoDB (via pymongo)**
```python
from pymongo import MongoClient

client = MongoClient("mongodb://localhost:27017/")
db = client["glorystone"]
collection = db["orders"]

# Insert
collection.insert_one({"order_id": 101, "status": "fulfilled"})

# Query
results = collection.find({"status": "fulfilled"})
for doc in results:
    print(doc)
```

### Packages & Modules

```python
# Import a module
import math
from math import sqrt, pi
import pandas as pd
import numpy as np

# Create your own module: save functions in my_utils.py then
from my_utils import clean_data, calculate_metrics
```

**Essential Data Stack**
| Package     | Purpose                          |
|-------------|----------------------------------|
| pandas      | DataFrames, cleaning, analysis   |
| numpy       | Numerical arrays & math          |
| matplotlib  | Plotting                         |
| seaborn     | Statistical visualizations       |
| scikit-learn| Machine learning                 |
| sqlalchemy  | Database abstraction             |
| requests    | HTTP / APIs                      |
| openpyxl    | Excel read/write                 |

### DSA Libraries (when needed)

- **collections**: `Counter`, `defaultdict`, `deque`, `namedtuple`
- **heapq**: priority queues
- **bisect**: binary search on sorted lists
- **itertools**: permutations, combinations, grouping
- **functools**: `lru_cache`, `partial`, `reduce`

```python
from collections import Counter, defaultdict
from itertools import combinations, groupby
```

---

## Quick Patterns for Data Work

```python
# Read CSV with pandas
import pandas as pd
df = pd.read_csv("glorystone_online_pickup_orders.csv")

# Basic exploration
df.head()
df.info()
df.describe()
df["column"].value_counts()

# Filtering
df[df["status"] == "fulfilled"]
df.query("wait_time > 30")

# Grouping
df.groupby("region")["revenue"].mean()

# Missing data
df.isna().sum()
df.dropna()
df.fillna(0)
```

---

*Reference built for Domain Specialist work – Glorystone Data Analytics track.*
