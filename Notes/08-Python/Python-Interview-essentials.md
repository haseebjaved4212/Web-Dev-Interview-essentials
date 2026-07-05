# 🐍 Python Interview Essentials

> A complete, beginner-friendly reference guide covering every Python concept you need to ace backend, data, and full-stack developer interviews. Written in simple, easy English with clear code examples and real-world patterns.

---

## 📌 Table of Contents

- [What is Python?](#what-is-python)
- [Variables and Data Types](#variables-and-data-types)
- [Strings](#strings)
- [Numbers and Math](#numbers-and-math)
- [Lists](#lists)
- [Tuples](#tuples)
- [Sets](#sets)
- [Dictionaries](#dictionaries)
- [Type Conversion](#type-conversion)
- [Operators](#operators)
- [Control Flow](#control-flow)
- [Functions](#functions)
- [Scope and Closures](#scope-and-closures)
- [Decorators](#decorators)
- [Comprehensions](#comprehensions)
- [Lambda Functions](#lambda-functions)
- [Object Oriented Programming](#object-oriented-programming)
- [Inheritance and Polymorphism](#inheritance-and-polymorphism)
- [Dunder Methods](#dunder-methods)
- [Iterators and Generators](#iterators-and-generators)
- [Context Managers](#context-managers)
- [Modules and Packages](#modules-and-packages)
- [File Handling](#file-handling)
- [Exception Handling](#exception-handling)
- [Regular Expressions](#regular-expressions)
- [Functional Programming](#functional-programming)
- [Concurrency and Parallelism](#concurrency-and-parallelism)
- [Type Hints](#type-hints)
- [Python Memory Management](#python-memory-management)
- [Common Built-in Functions](#common-built-in-functions)
- [Common Standard Library Modules](#common-standard-library-modules)
- [Best Practices and Pythonic Code](#best-practices-and-pythonic-code)
- [Common Interview Questions](#common-interview-questions)

---

## What is Python?

Python is a **high-level, interpreted, dynamically typed, general-purpose programming language**. It was created by Guido van Rossum and released in 1991. Python focuses on readability and simplicity, following the philosophy "there should be one obvious way to do it."

Key characteristics of Python:

- **Interpreted** - code runs line by line, no compile step needed
- **Dynamically typed** - you do not declare types, Python figures them out at runtime
- **Garbage collected** - memory is managed automatically
- **Multi-paradigm** - supports procedural, object-oriented, and functional styles
- **Huge standard library** - batteries included, tons built in
- **Cross-platform** - runs on Windows, Mac, Linux

Python is used for web backends (Django, FastAPI, Flask), data science, machine learning, automation, scripting, DevOps, and much more.

---

## Variables and Data Types

```python
# No need to declare types, just assign
name = "Haseeb"
age = 23
height = 5.9
is_active = True
nothing = None

# Python has 4 built-in collection types
my_list  = [1, 2, 3]       # ordered, mutable, allows duplicates
my_tuple = (1, 2, 3)       # ordered, immutable, allows duplicates
my_set   = {1, 2, 3}       # unordered, mutable, NO duplicates
my_dict  = {"key": "val"}  # key-value pairs, ordered (Python 3.7+), mutable

# Check the type of any variable
print(type(name))       # <class 'str'>
print(type(age))        # <class 'int'>
print(type(height))     # <class 'float'>
print(type(is_active))  # <class 'bool'>
print(type(nothing))    # <class 'NoneType'>

# Multiple assignment
x = y = z = 0
a, b, c = 1, 2, 3   # unpacking

# Swap two variables (Pythonic way, no temp variable needed)
a, b = b, a
```

---

## Strings

Strings in Python are immutable sequences of characters. They come with a huge number of built-in methods.

```python
# Creating strings
single = 'Hello'
double = "World"
multiline = """
This spans
multiple lines
"""

# f-strings (the modern, preferred way to format strings)
name = "Haseeb"
age = 23
print(f"My name is {name} and I am {age} years old")
print(f"Next year I will be {age + 1}")
print(f"Name uppercased: {name.upper()}")
print(f"Pi is approximately {3.14159:.2f}")  # format to 2 decimal places

# Common string methods
s = "  Hello, World!  "

s.strip()           # "Hello, World!" -- removes whitespace from both ends
s.lstrip()          # "Hello, World!  " -- removes from left only
s.rstrip()          # "  Hello, World!" -- removes from right only
s.upper()           # "  HELLO, WORLD!  "
s.lower()           # "  hello, world!  "
s.title()           # "  Hello, World!  "
s.replace("World", "Python")  # "  Hello, Python!  "
s.split(",")        # ["  Hello", " World!  "]
s.strip().split()   # ["Hello,", "World!"]
"hello".startswith("he")  # True
"hello".endswith("lo")    # True
"hello world".find("world")    # 6 -- index of first match, -1 if not found
"hello world".index("world")   # 6 -- same but raises ValueError if not found
"hello world".count("l")       # 3
"hello".center(11)             # "   hello   "
"hello".ljust(10, "-")         # "hello-----"
"hello".rjust(10, "-")         # "-----hello"
",".join(["a", "b", "c"])      # "a,b,c"
"abc".isalpha()    # True
"123".isdigit()    # True
"abc123".isalnum() # True
"  ".isspace()     # True

# String slicing [start:stop:step]
s = "Hello, World!"
s[0]       # "H"
s[-1]      # "!"
s[0:5]     # "Hello"
s[7:]      # "World!"
s[:5]      # "Hello"
s[::2]     # "Hlo ol!"  -- every 2nd character
s[::-1]    # "!dlroW ,olleH"  -- reverse

# Strings are immutable -- this fails
# s[0] = "h"   # TypeError

# Check if substring is in string
"World" in "Hello, World!"   # True
"xyz"   in "Hello, World!"   # False

# String multiplication
"Ha" * 3   # "HaHaHa"

# Raw strings (useful for regex and file paths)
path  = r"C:\Users\Haseeb\Documents"
regex = r"\d+\.\d+"
```

---

## Numbers and Math

```python
# Integer
x = 10
y = 3

# Basic arithmetic
x + y    # 13
x - y    # 7
x * y    # 30
x / y    # 3.3333... (always float in Python 3)
x // y   # 3 (floor division, rounds down)
x % y    # 1 (modulo, remainder)
x ** y   # 1000 (exponentiation)

# Float
pi = 3.14159
import math
math.floor(3.9)    # 3
math.ceil(3.1)     # 4
math.sqrt(16)      # 4.0
math.pow(2, 10)    # 1024.0
math.log(100, 10)  # 2.0
math.pi            # 3.141592653589793
abs(-5)            # 5
round(3.14159, 2)  # 3.14

# Integer limits (Python ints have no size limit, unlike most languages)
big = 10 ** 100    # no overflow, just works!

# Complex numbers
c = 3 + 4j
c.real   # 3.0
c.imag   # 4.0

# Useful number functions
max(1, 5, 3)          # 5
min(1, 5, 3)          # 1
sum([1, 2, 3, 4])     # 10
divmod(10, 3)         # (3, 1) -- quotient and remainder
pow(2, 10, 1000)      # 24 -- (2**10) % 1000, fast modular exponentiation

# Underscores in numbers for readability
big_number = 1_000_000
pi = 3.141_592_653
```

---

## Lists

Lists are ordered, mutable sequences. They are one of the most used data structures in Python.

```python
# Creating lists
fruits = ["apple", "banana", "cherry"]
mixed  = [1, "hello", True, None, [1, 2]]  # lists can hold different types
empty  = []
from_range = list(range(5))   # [0, 1, 2, 3, 4]

# Accessing elements
fruits[0]    # "apple"
fruits[-1]   # "cherry" (last element)
fruits[-2]   # "banana" (second to last)

# Slicing
fruits[0:2]  # ["apple", "banana"]
fruits[1:]   # ["banana", "cherry"]
fruits[::-1] # ["cherry", "banana", "apple"] -- reversed

# Modifying
fruits.append("mango")            # add to end
fruits.insert(1, "orange")        # insert at index
fruits.extend(["grape", "kiwi"])  # add multiple items
fruits.remove("banana")           # remove first occurrence of value
popped = fruits.pop()             # remove and return last item
popped = fruits.pop(0)            # remove and return item at index 0
fruits[0] = "avocado"             # update by index
del fruits[0]                     # delete by index
fruits.clear()                    # empty the list

# Searching and sorting
fruits = ["cherry", "apple", "banana"]
fruits.index("apple")    # 1 -- index of first occurrence
fruits.count("apple")    # 1 -- count occurrences
"apple" in fruits        # True

fruits.sort()            # sorts in place: ["apple", "banana", "cherry"]
fruits.sort(reverse=True)
fruits.reverse()         # reverse in place

sorted(fruits)           # returns a NEW sorted list, original unchanged
sorted(fruits, reverse=True)
sorted(fruits, key=str.lower)  # case-insensitive sort

# Copying (important: assignment is NOT a copy!)
original = [1, 2, 3]
ref = original           # same list, NOT a copy! Changes to ref affect original
copy = original.copy()   # shallow copy
copy = original[:]       # also a shallow copy
import copy
deep = copy.deepcopy(original)  # deep copy (needed for nested lists)

# Length, min, max, sum
nums = [3, 1, 4, 1, 5, 9]
len(nums)    # 6
min(nums)    # 1
max(nums)    # 9
sum(nums)    # 23

# Flattening a list of lists
nested = [[1, 2], [3, 4], [5, 6]]
flat = [item for sublist in nested for item in sublist]  # [1, 2, 3, 4, 5, 6]

# Unpacking
first, *rest = [1, 2, 3, 4]
# first = 1, rest = [2, 3, 4]

first, *middle, last = [1, 2, 3, 4, 5]
# first = 1, middle = [2, 3, 4], last = 5
```

---

## Tuples

Tuples are ordered and immutable. Use them for data that should not change.

```python
# Creating tuples
point   = (10, 20)
rgb     = (255, 128, 0)
single  = (42,)     # need a trailing comma for a single-element tuple
empty   = ()

# Tuples support indexing and slicing just like lists
point[0]   # 10
point[-1]  # 20
point[0:1] # (10,)

# Unpacking (very common in Python)
x, y = point
r, g, b = rgb

# Swap values using tuples
a, b = 1, 2
a, b = b, a   # a = 2, b = 1

# Tuple methods
rgb.index(128)   # 1
rgb.count(255)   # 1

# Convert between list and tuple
list_version  = list(point)   # [10, 20]
tuple_version = tuple([1, 2]) # (1, 2)

# Named tuples (gives names to positions -- very readable)
from collections import namedtuple

Point = namedtuple("Point", ["x", "y"])
p = Point(10, 20)
p.x    # 10
p.y    # 20
p[0]   # 10 (still works with index)
```

> **Interview Tip:** A common question is "When should you use a tuple vs a list?" The answer is: use a tuple when the data should not change (coordinates, RGB values, database records) and when you want to use it as a dictionary key (tuples are hashable, lists are not). Use a list when you need to add, remove, or change items.

---

## Sets

Sets are unordered collections of unique items. Great for removing duplicates and fast membership testing.

```python
# Creating sets
fruits = {"apple", "banana", "cherry"}
nums   = {1, 2, 3, 2, 1}   # duplicates removed: {1, 2, 3}
empty  = set()              # NOT {} -- that creates an empty dict!

# Adding and removing
fruits.add("mango")
fruits.update(["grape", "kiwi"])   # add multiple items
fruits.remove("banana")            # raises KeyError if not found
fruits.discard("banana")           # safe remove, no error if not found
popped = fruits.pop()              # removes and returns a random element

# Membership testing (O(1), much faster than list which is O(n))
"apple" in fruits   # True

# Set operations (classic math set theory)
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}

a | b             # union: {1, 2, 3, 4, 5, 6} -- all elements from both
a & b             # intersection: {3, 4} -- only in both
a - b             # difference: {1, 2} -- in a but NOT in b
b - a             # difference: {5, 6} -- in b but NOT in a
a ^ b             # symmetric difference: {1, 2, 5, 6} -- in one but NOT both

# Method versions (same thing)
a.union(b)
a.intersection(b)
a.difference(b)
a.symmetric_difference(b)

# Subset and superset checks
{1, 2}.issubset({1, 2, 3})    # True
{1, 2, 3}.issuperset({1, 2})  # True
{1, 2}.isdisjoint({3, 4})     # True -- no common elements

# Remove duplicates from a list (classic use case)
nums = [1, 2, 2, 3, 3, 3, 4]
unique_nums = list(set(nums))  # [1, 2, 3, 4] (order not guaranteed)
```

---

## Dictionaries

Dictionaries are key-value pairs. In Python 3.7+ they are ordered by insertion order.

```python
# Creating dictionaries
user = {"name": "Haseeb", "age": 23, "city": "Karachi"}
empty = {}
from_pairs = dict([("a", 1), ("b", 2)])
from_kwargs = dict(name="Haseeb", age=23)

# Accessing values
user["name"]            # "Haseeb" -- raises KeyError if not found
user.get("name")        # "Haseeb" -- returns None if not found
user.get("phone", "N/A")  # "N/A" -- default value if key not found

# Adding and updating
user["email"] = "h@test.com"      # add new key
user["age"] = 24                  # update existing key
user.update({"city": "Lahore", "phone": "123"})  # update multiple keys
user.setdefault("role", "user")   # set only if key does not exist

# Removing
del user["city"]
removed = user.pop("age")         # remove and return value
user.pop("missing", None)         # safe pop with default
user.popitem()                    # remove and return last inserted key-value pair
user.clear()                      # empty the dictionary

# Looping
user = {"name": "Haseeb", "age": 23}
for key in user:                  # iterates over keys
    print(key)

for key, value in user.items():   # iterates over key-value pairs
    print(f"{key}: {value}")

for value in user.values():       # iterates over values
    print(value)

# Dictionary methods
user.keys()     # dict_keys(["name", "age"]) -- a view object
user.values()   # dict_values(["Haseeb", 23])
user.items()    # dict_items([("name", "Haseeb"), ("age", 23)])

# Checking membership (checks keys by default)
"name" in user    # True
"phone" in user   # False

# Merging dictionaries
defaults = {"color": "blue", "size": "medium"}
overrides = {"color": "red"}

# Python 3.9+ merge operator
merged = defaults | overrides   # {"color": "red", "size": "medium"}

# Works in all Python 3.x
merged = {**defaults, **overrides}  # same result

# Nested dictionaries
config = {
    "database": {
        "host": "localhost",
        "port": 5432,
    },
    "cache": {
        "backend": "redis",
    }
}
config["database"]["host"]   # "localhost"

# Dictionary from two lists
keys   = ["name", "age", "city"]
values = ["Haseeb", 23, "Karachi"]
combined = dict(zip(keys, values))
# {"name": "Haseeb", "age": 23, "city": "Karachi"}
```

---

## Type Conversion

```python
# To integer
int("42")      # 42
int(3.9)       # 3 (truncates, does NOT round)
int(True)      # 1
int(False)     # 0
int("0xFF", 16)  # 255 (hex to int)
int("0b1010", 2) # 10  (binary to int)

# To float
float("3.14")  # 3.14
float(5)       # 5.0
float("inf")   # infinity

# To string
str(42)        # "42"
str(3.14)      # "3.14"
str(True)      # "True"
str(None)      # "None"

# To boolean
bool(0)        # False
bool("")       # False
bool(None)     # False
bool([])       # False
bool({})       # False
bool(1)        # True
bool("hello")  # True
bool([1])      # True

# To list, tuple, set
list("hello")          # ["h", "e", "l", "l", "o"]
list((1, 2, 3))        # [1, 2, 3]
list({1, 2, 3})        # [1, 2, 3] (order not guaranteed)
tuple([1, 2, 3])       # (1, 2, 3)
set([1, 2, 2, 3])      # {1, 2, 3}
```

---

## Operators

```python
# Arithmetic
5 + 2    # 7
5 - 2    # 3
5 * 2    # 10
5 / 2    # 2.5  (true division)
5 // 2   # 2    (floor division)
5 % 2    # 1    (modulo)
5 ** 2   # 25   (exponentiation)

# Comparison (all return True or False)
5 == 5   # True
5 != 3   # True
5 > 3    # True
5 < 3    # False
5 >= 5   # True
5 <= 4   # False

# Python allows chained comparisons (unlike most languages)
1 < 2 < 3       # True  (reads naturally)
10 > 5 > 2      # True
1 < x < 10      # checks if x is between 1 and 10

# Logical operators
True and False   # False
True or False    # True
not True         # False

# and/or return actual values, not just True/False
"hello" and "world"   # "world" (returns last truthy value)
"" and "world"        # "" (returns first falsy value)
"" or "default"       # "default" (returns first truthy value)
None or 0 or "value"  # "value"

# Identity operators (checks if TWO variables point to the SAME object)
a = [1, 2, 3]
b = a
c = [1, 2, 3]

a is b    # True  (same object in memory)
a is c    # False (different objects, same value)
a == c    # True  (same value)

# NEVER use 'is' to compare values -- use 'is' only for None, True, False
x is None    # correct way to check for None
x == None    # works but style guides say use 'is'

# Membership operators
"apple" in ["apple", "banana"]   # True
"grape" not in ["apple", "banana"]  # True
"he" in "hello"   # True (works on strings too)
3 in {1: "a", 2: "b", 3: "c"}  # True (checks keys in dict)

# Bitwise operators
5 & 3   # 1   (AND)
5 | 3   # 7   (OR)
5 ^ 3   # 6   (XOR)
~5      # -6  (NOT)
5 << 1  # 10  (left shift)
5 >> 1  # 2   (right shift)

# Walrus operator (Python 3.8+) -- assigns AND tests in one line
import re
if match := re.search(r"\d+", "Hello123"):
    print(match.group())  # "123"

# Useful in while loops
while chunk := file.read(1024):
    process(chunk)
```

---

## Control Flow

```python
# if / elif / else
score = 85

if score >= 90:
    grade = "A"
elif score >= 80:
    grade = "B"
elif score >= 70:
    grade = "C"
else:
    grade = "F"

# Ternary expression (one-liner if/else)
status = "adult" if age >= 18 else "minor"

# for loop
for i in range(5):        # 0, 1, 2, 3, 4
    print(i)

for i in range(1, 6):     # 1, 2, 3, 4, 5
    print(i)

for i in range(0, 10, 2): # 0, 2, 4, 6, 8
    print(i)

for item in ["a", "b", "c"]:
    print(item)

# enumerate gives you index AND value
for index, item in enumerate(["a", "b", "c"]):
    print(index, item)   # 0 a, 1 b, 2 c

for index, item in enumerate(["a", "b"], start=1):
    print(index, item)   # 1 a, 2 b

# zip combines two iterables
names  = ["Alice", "Bob", "Charlie"]
scores = [90, 85, 92]
for name, score in zip(names, scores):
    print(f"{name}: {score}")

# while loop
count = 0
while count < 5:
    print(count)
    count += 1

# break, continue, pass
for i in range(10):
    if i == 3:
        continue   # skip to next iteration
    if i == 7:
        break      # exit the loop completely
    print(i)

# pass -- does nothing, used as a placeholder
def todo_function():
    pass   # will implement later

# for...else and while...else (runs if loop completed without break)
for item in [1, 2, 3]:
    if item == 5:
        break
else:
    print("5 was not found")  # this DOES run because break was not hit

# match statement (Python 3.10+ -- like switch/case in other languages)
command = "quit"

match command:
    case "quit":
        print("Quitting")
    case "help":
        print("Showing help")
    case _:
        print(f"Unknown command: {command}")

# match with patterns
point = (1, 0)
match point:
    case (0, 0):
        print("Origin")
    case (x, 0):
        print(f"On X axis at {x}")
    case (0, y):
        print(f"On Y axis at {y}")
    case (x, y):
        print(f"Point at ({x}, {y})")
```

---

## Functions

```python
# Basic function
def greet(name):
    return f"Hello, {name}!"

# Default parameters
def greet(name, greeting="Hello"):
    return f"{greeting}, {name}!"

greet("Haseeb")           # "Hello, Haseeb!"
greet("Haseeb", "Hi")     # "Hi, Haseeb!"

# Multiple return values (actually returns a tuple)
def min_max(numbers):
    return min(numbers), max(numbers)

low, high = min_max([3, 1, 4, 1, 5])

# *args -- collects extra POSITIONAL arguments into a tuple
def sum_all(*args):
    return sum(args)

sum_all(1, 2, 3, 4, 5)  # 15

# **kwargs -- collects extra KEYWORD arguments into a dictionary
def print_info(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")

print_info(name="Haseeb", age=23, city="Karachi")

# Combining all parameter types
def func(required, default="default", *args, **kwargs):
    print(required, default, args, kwargs)

func("a", "b", "c", "d", x=1, y=2)
# "a", "b", ("c", "d"), {"x": 1, "y": 2}

# Keyword-only arguments (after *)
def greet(name, *, greeting="Hello"):
    return f"{greeting}, {name}"
# greet("Haseeb", "Hi")     # Error: positional not allowed after *
greet("Haseeb", greeting="Hi")  # must use keyword

# Positional-only arguments (before /)  Python 3.8+
def add(x, y, /):
    return x + y
# add(x=1, y=2)  # Error: must be positional

# Function annotations (type hints)
def add(x: int, y: int) -> int:
    return x + y

# Docstrings
def calculate_area(radius: float) -> float:
    """
    Calculate the area of a circle.

    Args:
        radius: The radius of the circle.

    Returns:
        The area of the circle.
    """
    import math
    return math.pi * radius ** 2
```

---

## Scope and Closures

```python
# LEGB rule: Python looks for names in this order
# Local -> Enclosing -> Global -> Built-in

x = "global"

def outer():
    x = "enclosing"

    def inner():
        x = "local"
        print(x)   # "local"

    inner()
    print(x)   # "enclosing"

print(x)   # "global"

# global keyword: access and modify a global variable inside a function
count = 0

def increment():
    global count
    count += 1

increment()
print(count)  # 1

# nonlocal keyword: access and modify an enclosing scope variable
def make_counter():
    count = 0

    def increment():
        nonlocal count
        count += 1
        return count

    return increment

counter = make_counter()
counter()  # 1
counter()  # 2
counter()  # 3
# count is NOT accessible here, it is private to make_counter

# Closures: a function that "remembers" the variables from its enclosing scope
def multiplier(factor):
    def multiply(number):
        return number * factor   # "remembers" factor even after multiplier returns
    return multiply

double = multiplier(2)
triple = multiplier(3)

double(5)   # 10
triple(5)   # 15
```

---

## Decorators

A decorator is a function that **takes another function and adds behavior to it without changing its code**. They are used heavily in frameworks like Django, Flask, and FastAPI.

```python
# Basic decorator
def log_calls(func):
    def wrapper(*args, **kwargs):
        print(f"Calling {func.__name__}")
        result = func(*args, **kwargs)
        print(f"{func.__name__} returned {result}")
        return result
    return wrapper

@log_calls
def add(a, b):
    return a + b

add(3, 4)
# Calling add
# add returned 7
# 7

# This is EXACTLY the same as:
# add = log_calls(add)

# Preserving function metadata with functools.wraps
from functools import wraps

def log_calls(func):
    @wraps(func)   # preserves __name__, __doc__ etc.
    def wrapper(*args, **kwargs):
        print(f"Calling {func.__name__}")
        result = func(*args, **kwargs)
        return result
    return wrapper

# Decorator with arguments
def repeat(times):
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            for _ in range(times):
                result = func(*args, **kwargs)
            return result
        return wrapper
    return decorator

@repeat(3)
def say_hello():
    print("Hello!")

say_hello()  # prints "Hello!" 3 times

# Real-world examples
def require_auth(func):
    @wraps(func)
    def wrapper(request, *args, **kwargs):
        if not request.user.is_authenticated:
            raise PermissionError("Login required")
        return func(request, *args, **kwargs)
    return wrapper

def timer(func):
    import time
    @wraps(func)
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f"{func.__name__} took {end - start:.4f}s")
        return result
    return wrapper

# Stacking decorators (applied bottom-up)
@timer
@log_calls
def process_data(data):
    return data

# This is equivalent to:
# process_data = timer(log_calls(process_data))

# Class decorators
class Singleton:
    _instances = {}

    def __call__(cls, *args, **kwargs):
        if cls not in cls._instances:
            cls._instances[cls] = super().__call__(*args, **kwargs)
        return cls._instances[cls]
```

---

## Comprehensions

Comprehensions are a concise way to create lists, dictionaries, and sets. They are one of the most Pythonic features.

```python
# List comprehension [expression for item in iterable if condition]
squares   = [x**2 for x in range(10)]
# [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

evens     = [x for x in range(20) if x % 2 == 0]
# [0, 2, 4, 6, 8, 10, 12, 14, 16, 18]

names     = ["  Haseeb  ", "  Ahmed  "]
cleaned   = [name.strip() for name in names]

# Nested list comprehension
matrix    = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
flat      = [num for row in matrix for num in row]
# [1, 2, 3, 4, 5, 6, 7, 8, 9]

# With conditional expression (ternary)
labels = ["even" if x % 2 == 0 else "odd" for x in range(5)]
# ["even", "odd", "even", "odd", "even"]

# Dictionary comprehension {key_expr: val_expr for item in iterable}
word_lengths = {word: len(word) for word in ["apple", "banana", "cherry"]}
# {"apple": 5, "banana": 6, "cherry": 6}

squared_dict = {x: x**2 for x in range(5)}
# {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}

inverted = {v: k for k, v in {"a": 1, "b": 2}.items()}
# {1: "a", 2: "b"}

# Set comprehension {expression for item in iterable}
unique_lengths = {len(word) for word in ["cat", "dog", "bird", "ant"]}
# {3, 4}

# Generator expression (memory efficient -- lazy evaluation)
# Uses () instead of []
gen = (x**2 for x in range(1000000))  # does NOT create a million items in memory
next(gen)    # 0
next(gen)    # 1
sum(x**2 for x in range(100))  # works without building a list first
```

---

## Lambda Functions

Lambda functions are small, anonymous (nameless) functions defined in one line.

```python
# Basic lambda
square = lambda x: x ** 2
square(5)  # 25

add = lambda a, b: a + b
add(3, 4)  # 7

# Most common use: as a key function for sorting
students = [
    {"name": "Haseeb", "grade": 85},
    {"name": "Ahmed",  "grade": 92},
    {"name": "Sara",   "grade": 78},
]

students.sort(key=lambda s: s["grade"])
# sorted by grade ascending

sorted(students, key=lambda s: s["grade"], reverse=True)
# sorted by grade descending

# Sorting by multiple criteria
people = [("Haseeb", 23), ("Ahmed", 25), ("Sara", 23)]
people.sort(key=lambda p: (p[1], p[0]))  # sort by age, then name

# Used with filter(), map()
nums = [1, 2, 3, 4, 5, 6, 7, 8]
evens     = list(filter(lambda x: x % 2 == 0, nums))  # [2, 4, 6, 8]
doubled   = list(map(lambda x: x * 2, nums))           # [2, 4, 6, 8, 10, 12, 14, 16]
```

> **Interview Tip:** Lambdas are not always more readable. For simple sorting keys they are great. For anything more complex, a named function is clearer. Never use a lambda if the function needs a docstring or more than one expression.

---

## Object Oriented Programming

```python
class Animal:
    # Class variable (shared by all instances)
    kingdom = "Animalia"

    def __init__(self, name, age):
        # Instance variables (unique to each object)
        self.name = name
        self.age = age
        self._secret = "hidden"   # convention: "private" (single underscore)
        self.__mangled = "very private"  # name-mangled (double underscore)

    # Instance method
    def speak(self):
        return f"{self.name} makes a sound"

    # Class method (works on the class, not an instance)
    @classmethod
    def create(cls, name):
        return cls(name, 0)   # alternate constructor

    # Static method (no access to class or instance, just a utility)
    @staticmethod
    def is_alive():
        return True

    # String representation
    def __str__(self):
        return f"Animal(name={self.name}, age={self.age})"

    def __repr__(self):
        return f"Animal({self.name!r}, {self.age!r})"


# Creating objects
cat = Animal("Whiskers", 3)
dog = Animal.create("Rex")   # using class method

# Accessing attributes and methods
cat.name             # "Whiskers"
cat.speak()          # "Whiskers makes a sound"
Animal.kingdom       # "Animalia"
cat.kingdom          # also works, looks up class variable
Animal.is_alive()    # True
cat.is_alive()       # also works

# Properties: control attribute access with getter/setter
class Temperature:
    def __init__(self, celsius=0):
        self._celsius = celsius

    @property
    def celsius(self):
        return self._celsius

    @celsius.setter
    def celsius(self, value):
        if value < -273.15:
            raise ValueError("Below absolute zero!")
        self._celsius = value

    @property
    def fahrenheit(self):
        return (self._celsius * 9 / 5) + 32

    @fahrenheit.setter
    def fahrenheit(self, value):
        self.celsius = (value - 32) * 5 / 9


temp = Temperature(25)
temp.celsius     # 25
temp.fahrenheit  # 77.0
temp.celsius = 100
# temp.celsius = -300  # raises ValueError
```

---

## Inheritance and Polymorphism

```python
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        raise NotImplementedError("Subclasses must implement speak()")

    def describe(self):
        return f"I am {self.name}"


class Dog(Animal):
    def speak(self):
        return f"{self.name} says Woof!"

    def fetch(self):
        return f"{self.name} fetches the ball"


class Cat(Animal):
    def speak(self):
        return f"{self.name} says Meow!"


class Duck(Animal):
    def speak(self):
        return f"{self.name} says Quack!"


# Polymorphism: same method call, different behavior
animals = [Dog("Rex"), Cat("Whiskers"), Duck("Donald")]
for animal in animals:
    print(animal.speak())  # each prints differently

# isinstance and issubclass
isinstance(Dog("Rex"), Dog)     # True
isinstance(Dog("Rex"), Animal)  # True (also an Animal)
issubclass(Dog, Animal)         # True

# super() -- calling the parent class method
class GuideDog(Dog):
    def __init__(self, name, owner):
        super().__init__(name)   # call parent __init__
        self.owner = owner

    def speak(self):
        return super().speak() + " (I am a guide dog)"

    def describe(self):
        parent_desc = super().describe()
        return f"{parent_desc}, and I guide {self.owner}"


# Multiple inheritance
class Flyable:
    def fly(self):
        return "I can fly"

class Swimmable:
    def swim(self):
        return "I can swim"

class Duck2(Animal, Flyable, Swimmable):
    def speak(self):
        return "Quack!"

donald = Duck2("Donald")
donald.fly()   # "I can fly"
donald.swim()  # "I can swim"
donald.speak() # "Quack!"

# MRO (Method Resolution Order) -- the order Python looks up methods
Duck2.__mro__
# (<class 'Duck2'>, <class 'Animal'>, <class 'Flyable'>, <class 'Swimmable'>, <class 'object'>)

# Abstract classes: enforce that subclasses implement certain methods
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self) -> float:
        pass

    @abstractmethod
    def perimeter(self) -> float:
        pass

    def describe(self):
        return f"Area: {self.area()}, Perimeter: {self.perimeter()}"

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        import math
        return math.pi * self.radius ** 2

    def perimeter(self):
        import math
        return 2 * math.pi * self.radius

# shape = Shape()  # TypeError: cannot instantiate abstract class
circle = Circle(5)
circle.area()       # 78.53...
circle.describe()   # "Area: 78.53..., Perimeter: 31.41..."
```

---

## Dunder Methods

Dunder (double underscore) methods, also called magic methods, let you customize how your objects behave with built-in operators and functions.

```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    # String representation for end users (__str__)
    def __str__(self):
        return f"Vector({self.x}, {self.y})"

    # String representation for developers (__repr__)
    def __repr__(self):
        return f"Vector(x={self.x!r}, y={self.y!r})"

    # Addition: v1 + v2
    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)

    # Subtraction: v1 - v2
    def __sub__(self, other):
        return Vector(self.x - other.x, self.y - other.y)

    # Multiplication: v * scalar
    def __mul__(self, scalar):
        return Vector(self.x * scalar, self.y * scalar)

    # Equality: v1 == v2
    def __eq__(self, other):
        return self.x == other.x and self.y == other.y

    # Length: len(v)
    def __len__(self):
        return 2

    # Absolute value: abs(v)
    def __abs__(self):
        return (self.x**2 + self.y**2) ** 0.5

    # Make iterable: for component in v
    def __iter__(self):
        yield self.x
        yield self.y

    # Item access: v[0]
    def __getitem__(self, index):
        return (self.x, self.y)[index]

    # Boolean check: if v
    def __bool__(self):
        return self.x != 0 or self.y != 0

    # Make hashable (needed to use as dict key or in set)
    def __hash__(self):
        return hash((self.x, self.y))

    # Context manager support
    def __enter__(self):
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        return False

v1 = Vector(1, 2)
v2 = Vector(3, 4)

print(v1)       # "Vector(1, 2)"
v1 + v2         # Vector(4, 6)
v1 == Vector(1, 2)  # True
abs(v2)         # 5.0
list(v1)        # [1, 2]
```

| Dunder Method | What it does |
|---|---|
| `__init__` | Constructor, called on object creation |
| `__str__` | `str(obj)` and `print(obj)` |
| `__repr__` | Unambiguous representation, used in REPL |
| `__len__` | `len(obj)` |
| `__eq__` | `obj1 == obj2` |
| `__lt__` | `obj1 < obj2` |
| `__add__` | `obj1 + obj2` |
| `__getitem__` | `obj[key]` |
| `__setitem__` | `obj[key] = value` |
| `__contains__` | `item in obj` |
| `__iter__` | `for item in obj` |
| `__next__` | `next(obj)` |
| `__call__` | `obj()` -- makes instance callable |
| `__enter__` | `with obj as x:` start |
| `__exit__` | `with obj as x:` end |

---

## Iterators and Generators

```python
# Iterator protocol: any object with __iter__() and __next__()
class CountUp:
    def __init__(self, start, end):
        self.current = start
        self.end = end

    def __iter__(self):
        return self   # this object IS the iterator

    def __next__(self):
        if self.current >= self.end:
            raise StopIteration
        value = self.current
        self.current += 1
        return value

for num in CountUp(1, 5):
    print(num)   # 1 2 3 4

# Generator functions: much simpler way to create iterators
# Uses yield instead of return
def count_up(start, end):
    current = start
    while current < end:
        yield current    # pause here, return value, resume next time
        current += 1

for num in count_up(1, 5):
    print(num)   # 1 2 3 4

# Generators are lazy -- they compute one value at a time
def infinite_sequence():
    num = 0
    while True:
        yield num
        num += 1

gen = infinite_sequence()
next(gen)   # 0
next(gen)   # 1
next(gen)   # 2

# Practical use: reading large files line by line
def read_large_file(filepath):
    with open(filepath) as f:
        for line in f:
            yield line.strip()  # one line at a time, not the whole file!

# yield from -- delegate to another iterable
def chain(*iterables):
    for iterable in iterables:
        yield from iterable   # same as: for item in iterable: yield item

list(chain([1, 2], [3, 4], [5, 6]))  # [1, 2, 3, 4, 5, 6]

# Generator expressions (like list comprehensions but lazy)
gen_exp = (x**2 for x in range(10))  # does NOT create list in memory
sum(gen_exp)   # 285

# itertools: powerful tools for working with iterators
import itertools

list(itertools.count(10, 2))         # infinite: 10, 12, 14, ...
list(itertools.cycle("ABC"))         # infinite: A, B, C, A, B, C, ...
list(itertools.repeat(0, 5))         # [0, 0, 0, 0, 0]
list(itertools.chain([1, 2], [3, 4]))  # [1, 2, 3, 4]
list(itertools.islice(range(100), 5))  # [0, 1, 2, 3, 4]
list(itertools.combinations([1,2,3], 2))  # [(1,2), (1,3), (2,3)]
list(itertools.permutations([1,2,3], 2))  # [(1,2), (1,3), (2,1), ...]
```

---

## Context Managers

Context managers handle setup and teardown automatically. The most common use is file handling, but they work for anything that needs clean-up.

```python
# Built-in context manager
with open("file.txt", "r") as f:
    content = f.read()
# File is automatically closed even if an exception occurs

# Creating a context manager with a class
class DatabaseConnection:
    def __init__(self, url):
        self.url = url
        self.connection = None

    def __enter__(self):
        self.connection = connect(self.url)
        return self.connection

    def __exit__(self, exc_type, exc_val, exc_tb):
        if self.connection:
            self.connection.close()
        return False   # False means "do not suppress exceptions"

with DatabaseConnection("postgresql://...") as conn:
    conn.execute("SELECT * FROM users")
# Connection is closed automatically

# Creating a context manager with contextlib (simpler)
from contextlib import contextmanager

@contextmanager
def timer():
    import time
    start = time.time()
    try:
        yield  # code inside 'with' block runs here
    finally:
        elapsed = time.time() - start
        print(f"Elapsed: {elapsed:.3f}s")

with timer():
    # some slow operation
    sum(range(1_000_000))

# Suppress specific exceptions
from contextlib import suppress

with suppress(FileNotFoundError):
    open("nonexistent.txt")  # this exception is silently ignored
```

---

## Modules and Packages

```python
# Importing modules
import math
import os
import sys

math.sqrt(16)      # 4.0
math.pi            # 3.141592...
os.getcwd()        # current working directory
os.path.join("a", "b", "c")   # "a/b/c" (or "a\\b\\c" on Windows)

# Import specific items from a module
from math import sqrt, pi
sqrt(16)   # 4.0 (no need for "math." prefix)

# Import with alias
import numpy as np
from datetime import datetime as dt

# Import everything (usually avoid this -- pollutes namespace)
from math import *

# Your own module
# In myutils.py:
def add(a, b):
    return a + b

PI = 3.14159

# In main.py:
import myutils
myutils.add(1, 2)

from myutils import add, PI

# __name__ == "__main__" (very important pattern)
# Code inside this block only runs when the file is executed directly,
# NOT when it is imported as a module
if __name__ == "__main__":
    print("This runs only when you run this file directly")

# Package: a folder with an __init__.py file
# mypackage/
#     __init__.py
#     module1.py
#     module2.py
#     subpackage/
#         __init__.py
#         module3.py

from mypackage import module1
from mypackage.subpackage import module3
```

---

## File Handling

```python
# Reading files
with open("file.txt", "r") as f:
    content = f.read()        # read entire file as string
    lines   = f.readlines()   # list of lines (each with \n)
    line    = f.readline()    # read one line at a time

# Iterating line by line (memory efficient)
with open("large_file.txt", "r") as f:
    for line in f:
        process(line.strip())

# Writing files
with open("output.txt", "w") as f:   # "w" overwrites if exists
    f.write("Hello, World!\n")
    f.writelines(["line1\n", "line2\n"])

with open("output.txt", "a") as f:   # "a" appends, does not overwrite
    f.write("New line\n")

# File modes
# "r"  = read (default)
# "w"  = write (overwrites)
# "a"  = append
# "rb" = read binary (images, PDFs, etc.)
# "wb" = write binary
# "r+" = read AND write

# Working with paths (use pathlib, the modern way)
from pathlib import Path

p = Path("documents/report.txt")
p.name           # "report.txt"
p.stem           # "report"
p.suffix         # ".txt"
p.parent         # Path("documents")
p.exists()       # True/False
p.is_file()      # True/False
p.is_dir()       # True/False

# Create directory
Path("new_folder").mkdir(parents=True, exist_ok=True)

# Read/write with pathlib
content = p.read_text()
p.write_text("Hello!")

# List files in a directory
for file in Path(".").iterdir():
    print(file)

# Glob patterns
for py_file in Path(".").glob("**/*.py"):  # all .py files recursively
    print(py_file)

# JSON files
import json

data = {"name": "Haseeb", "age": 23}

with open("data.json", "w") as f:
    json.dump(data, f, indent=2)

with open("data.json", "r") as f:
    loaded = json.load(f)

# CSV files
import csv

with open("data.csv", "w", newline="") as f:
    writer = csv.DictWriter(f, fieldnames=["name", "age"])
    writer.writeheader()
    writer.writerow({"name": "Haseeb", "age": 23})

with open("data.csv", "r") as f:
    reader = csv.DictReader(f)
    for row in reader:
        print(row)
```

---

## Exception Handling

```python
# Basic try/except
try:
    result = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero")

# Multiple exception types
try:
    value = int(input("Enter a number: "))
    result = 10 / value
except ValueError:
    print("That is not a number")
except ZeroDivisionError:
    print("Cannot divide by zero")
except (TypeError, IndexError) as e:
    print(f"Unexpected error: {e}")
except Exception as e:
    print(f"Something went wrong: {e}")
    raise   # re-raise the exception after logging

# else: runs if NO exception was raised
try:
    result = 10 / 2
except ZeroDivisionError:
    print("Error")
else:
    print(f"Result is {result}")  # this runs

# finally: ALWAYS runs, with or without exception (use for cleanup)
try:
    f = open("file.txt")
    data = f.read()
except FileNotFoundError:
    print("File not found")
finally:
    f.close()   # always closes, even if exception occurred

# Custom exceptions
class InsufficientFundsError(Exception):
    def __init__(self, amount, balance):
        self.amount = amount
        self.balance = balance
        super().__init__(f"Tried to withdraw {amount} but only have {balance}")

class NegativeAmountError(ValueError):
    pass

def withdraw(balance, amount):
    if amount < 0:
        raise NegativeAmountError("Amount cannot be negative")
    if amount > balance:
        raise InsufficientFundsError(amount, balance)
    return balance - amount

try:
    result = withdraw(100, 150)
except InsufficientFundsError as e:
    print(e)             # "Tried to withdraw 150 but only have 100"
    print(e.amount)      # 150
    print(e.balance)     # 100

# Exception chaining
try:
    value = int("not a number")
except ValueError as e:
    raise RuntimeError("Failed to process input") from e
    # This preserves the original error as the "cause"

# assert (useful for debugging and tests)
def get_user(id):
    assert isinstance(id, int), f"id must be int, got {type(id)}"
    # ... rest of function
```

---

## Regular Expressions

```python
import re

text = "My phone is 0300-1234567 and email is haseeb@example.com"

# Search for first match anywhere in string
match = re.search(r"\d{4}-\d{7}", text)
if match:
    print(match.group())    # "0300-1234567"
    print(match.start())    # index where match starts
    print(match.end())      # index where match ends

# Find ALL matches
phones = re.findall(r"\d{4}-\d{7}", text)   # list of all matches

# Full string match (not just substring)
is_email = re.match(r"[\w.-]+@[\w.-]+\.\w+", "haseeb@example.com")

# Substitute
cleaned = re.sub(r"\s+", " ", "too   many    spaces")   # "too many spaces"

# Split by pattern
parts = re.split(r"[,;]\s*", "one, two; three,four")   # ["one", "two", "three", "four"]

# Compiled patterns (faster if used many times)
email_pattern = re.compile(r"[\w.-]+@[\w.-]+\.\w+")
matches = email_pattern.findall(text)

# Common regex patterns
r"\d"          # digit 0-9
r"\D"          # non-digit
r"\w"          # word character (letter, digit, underscore)
r"\W"          # non-word character
r"\s"          # whitespace (space, tab, newline)
r"\S"          # non-whitespace
r"."           # any character except newline
r"^"           # start of string
r"$"           # end of string
r"[abc]"       # a, b, or c
r"[a-z]"       # any lowercase letter
r"[^abc]"      # NOT a, b, or c
r"a+"          # one or more a
r"a*"          # zero or more a
r"a?"          # zero or one a
r"a{3}"        # exactly 3 a's
r"a{2,5}"      # 2 to 5 a's
r"(abc)"       # capture group
r"(?P<name>...)"  # named capture group
```

---

## Functional Programming

```python
# map: apply a function to every item in an iterable
nums    = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x**2, nums))   # [1, 4, 9, 16, 25]
strings = list(map(str, nums))              # ["1", "2", "3", "4", "5"]

# filter: keep only items where function returns True
evens   = list(filter(lambda x: x % 2 == 0, nums))  # [2, 4]
truthy  = list(filter(None, [0, 1, "", "hello", None, False, True]))  # [1, "hello", True]

# reduce: accumulate a result across all items
from functools import reduce
product = reduce(lambda acc, x: acc * x, [1, 2, 3, 4, 5])  # 120

# sorted with key
words = ["banana", "Apple", "cherry"]
sorted(words, key=str.lower)         # ["Apple", "banana", "cherry"]
sorted(words, key=len)               # ["Apple", "banana", "cherry"] by length

# functools.partial: fix some arguments of a function
from functools import partial

def power(base, exponent):
    return base ** exponent

square = partial(power, exponent=2)
cube   = partial(power, exponent=3)

square(4)  # 16
cube(3)    # 27

# functools.lru_cache: memoize expensive function results
from functools import lru_cache

@lru_cache(maxsize=None)
def fibonacci(n):
    if n < 2:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)

fibonacci(100)  # instant, results are cached

# Pure function example
def double_all(numbers):
    return [n * 2 for n in numbers]  # does NOT modify the original list

# Immutable data approach
original = (1, 2, 3)
doubled  = tuple(x * 2 for x in original)
```

---

## Concurrency and Parallelism

```python
# Threading: for I/O-bound tasks (network calls, file reading)
# Python threads are limited by the GIL for CPU tasks
import threading
import time

def fetch_data(url, results, index):
    # simulate network request
    time.sleep(1)
    results[index] = f"Data from {url}"

results = [None] * 3
threads = []

for i, url in enumerate(["url1", "url2", "url3"]):
    t = threading.Thread(target=fetch_data, args=(url, results, i))
    threads.append(t)
    t.start()

for t in threads:
    t.join()   # wait for all threads to finish

print(results)

# asyncio: for I/O-bound tasks (better than threads for many connections)
import asyncio
import aiohttp

async def fetch(session, url):
    async with session.get(url) as response:
        return await response.text()

async def main():
    urls = ["http://example.com", "http://example.org"]
    async with aiohttp.ClientSession() as session:
        tasks = [fetch(session, url) for url in urls]
        results = await asyncio.gather(*tasks)
    return results

asyncio.run(main())

# multiprocessing: for CPU-bound tasks (bypasses the GIL)
from multiprocessing import Pool

def process_chunk(chunk):
    return sum(x**2 for x in chunk)

if __name__ == "__main__":
    data = list(range(1_000_000))
    chunks = [data[i::4] for i in range(4)]  # split into 4 chunks

    with Pool(4) as pool:
        results = pool.map(process_chunk, chunks)

    total = sum(results)

# concurrent.futures: cleaner API for both threads and processes
from concurrent.futures import ThreadPoolExecutor, ProcessPoolExecutor

def download(url):
    return f"Content from {url}"

with ThreadPoolExecutor(max_workers=5) as executor:
    urls = ["url1", "url2", "url3"]
    results = list(executor.map(download, urls))
```

> **Interview Tip:** A very common question is "What is the GIL?" The GIL (Global Interpreter Lock) is a mutex in CPython that allows only one thread to execute Python bytecode at a time, even on multi-core machines. This means Python threads do NOT truly run in parallel for CPU-bound tasks. The fix is to use `multiprocessing` (separate processes bypass the GIL) for CPU work, and `asyncio` or `threading` for I/O work (where threads spend most of their time waiting, not executing).

---

## Type Hints

Python type hints (added in Python 3.5+) let you annotate your code with types. They do not enforce anything at runtime but help editors, linters, and other developers understand your code.

```python
from typing import List, Dict, Tuple, Optional, Union, Any, Callable

# Basic annotations
def greet(name: str) -> str:
    return f"Hello, {name}"

def add(a: int, b: int) -> int:
    return a + b

# Python 3.9+ built-in generics (no need to import from typing)
def process(items: list[int]) -> dict[str, int]:
    return {"total": sum(items)}

# Optional: value could be None
def find_user(id: int) -> Optional[dict]:   # old way
    pass

def find_user(id: int) -> dict | None:      # Python 3.10+ way
    pass

# Union: value could be one of multiple types
def process(value: Union[str, int]) -> str:   # old way
    return str(value)

def process(value: str | int) -> str:          # Python 3.10+ way
    return str(value)

# Any: no type checking
def do_something(data: Any) -> Any:
    return data

# Callable: typing functions
def apply(func: Callable[[int, int], int], a: int, b: int) -> int:
    return func(a, b)

# TypedDict: dictionary with known keys and types
from typing import TypedDict

class UserDict(TypedDict):
    name: str
    age: int
    email: str

def create_user(data: UserDict) -> UserDict:
    return data

# dataclass: clean way to create classes that are mostly data containers
from dataclasses import dataclass, field

@dataclass
class User:
    name: str
    age: int
    email: str
    tags: list[str] = field(default_factory=list)  # mutable defaults need field()
    active: bool = True

user = User(name="Haseeb", age=23, email="h@test.com")
user.name   # "Haseeb"
print(user) # User(name='Haseeb', age=23, email='h@test.com', tags=[], active=True)

@dataclass(frozen=True)  # immutable dataclass
class Point:
    x: float
    y: float
```

---

## Python Memory Management

```python
# Reference counting: Python tracks how many variables point to each object
import sys

x = [1, 2, 3]
y = x          # both x and y point to the SAME list
sys.getrefcount(x)  # 3 (x, y, and the function argument itself)

del y          # removes one reference
# when reference count reaches 0, memory is freed

# id() shows the memory address of an object
a = "hello"
b = "hello"
id(a) == id(b)  # True (Python interns small strings to save memory)

a = [1, 2]
b = [1, 2]
id(a) == id(b)  # False (different list objects)

# Mutable vs Immutable
# Immutable: int, float, str, tuple, bool, frozenset
# Mutable: list, dict, set, bytearray

# Mutation gotcha with default arguments
def add_item(item, my_list=[]):   # WRONG! mutable default is shared across calls
    my_list.append(item)
    return my_list

add_item(1)  # [1]
add_item(2)  # [1, 2]  -- NOT [2]! Same list is reused!

# Correct way
def add_item(item, my_list=None):
    if my_list is None:
        my_list = []
    my_list.append(item)
    return my_list

# Memory profiling
import tracemalloc

tracemalloc.start()
# ... run your code ...
snapshot = tracemalloc.take_snapshot()
```

---

## Common Built-in Functions

```python
# Type and conversion
type(x)         # get type of x
isinstance(x, int)  # check type safely
int(), float(), str(), bool(), list(), tuple(), set(), dict()

# Math
abs(-5)         # 5
round(3.567, 2) # 3.57
min(1, 2, 3)    # 1
max(1, 2, 3)    # 3
sum([1, 2, 3])  # 6
pow(2, 10)      # 1024
divmod(17, 5)   # (3, 2)

# Iteration helpers
range(5)           # 0, 1, 2, 3, 4
range(1, 6)        # 1, 2, 3, 4, 5
range(0, 10, 2)    # 0, 2, 4, 6, 8
enumerate(iterable, start=0)  # (index, value) pairs
zip(*iterables)    # combine iterables
reversed(seq)      # reverse iterator
sorted(iterable, key=None, reverse=False)
map(func, iterable)
filter(func, iterable)
any(iterable)      # True if at least one is truthy
all(iterable)      # True if ALL are truthy

# Object info
len(x)         # length
id(x)          # memory address
hash(x)        # hash value (only for immutable objects)
dir(x)         # list all attributes and methods
vars(x)        # __dict__ of an object
getattr(obj, "name", default)    # get attribute by name
setattr(obj, "name", value)
hasattr(obj, "name")
callable(obj)  # True if obj can be called like a function

# I/O
print(*objects, sep=" ", end="\n", file=sys.stdout)
input(prompt)  # reads a line from stdin as a string

# Misc
open(file, mode)
iter(obj)         # get iterator
next(iterator)    # get next item
repr(obj)         # developer-friendly string
format(value, spec)
eval("1 + 2")     # evaluates a string as Python code (be careful!)
exec("x = 5")     # executes a string as Python statements
```

---

## Common Standard Library Modules

```python
# collections: specialized data structures
from collections import Counter, defaultdict, OrderedDict, deque, namedtuple

Counter("hello world")   # Counter({'l': 3, 'o': 2, ...})
Counter([1,1,2,3,3,3])  # Counter({3: 3, 1: 2, 2: 1})
c.most_common(2)         # 2 most common items

d = defaultdict(list)    # default value is an empty list
d["missing"].append(1)   # no KeyError, creates key with []

queue = deque([1, 2, 3])
queue.appendleft(0)      # [0, 1, 2, 3]
queue.popleft()          # 0

# os: operating system interaction
import os
os.getcwd()
os.listdir(".")
os.path.join("folder", "file.txt")
os.path.exists("path")
os.path.isfile("path")
os.path.isdir("path")
os.makedirs("dir/subdir", exist_ok=True)
os.environ.get("HOME")
os.getenv("API_KEY", "default")

# sys: system-specific parameters
import sys
sys.argv           # command-line arguments
sys.path           # list of directories Python searches for modules
sys.exit(0)        # exit with code 0
sys.version        # Python version string

# datetime
from datetime import datetime, date, timedelta

now   = datetime.now()
today = date.today()
dt    = datetime(2024, 1, 15, 9, 30)
dt.strftime("%Y-%m-%d %H:%M")    # "2024-01-15 09:30"
datetime.strptime("2024-01-15", "%Y-%m-%d")

one_week_later = today + timedelta(days=7)
diff = datetime(2024, 12, 31) - datetime.now()
diff.days   # number of days until

# random
import random
random.random()            # float between 0 and 1
random.randint(1, 10)      # int between 1 and 10 inclusive
random.choice([1, 2, 3])   # random item from list
random.sample([1,2,3,4], 2)  # 2 unique random items
random.shuffle([1, 2, 3])  # shuffle list in place

# time
import time
time.time()         # Unix timestamp (seconds since 1970)
time.sleep(1.5)     # pause for 1.5 seconds

# copy
import copy
copy.copy(obj)       # shallow copy
copy.deepcopy(obj)   # deep copy

# hashlib: cryptographic hashing
import hashlib
hashlib.sha256("hello".encode()).hexdigest()  # hash of "hello"
hashlib.md5("hello".encode()).hexdigest()

# logging
import logging
logging.basicConfig(level=logging.INFO)
logging.debug("Debug message")
logging.info("Info message")
logging.warning("Warning!")
logging.error("Error!")
logging.critical("Critical!")
```

---

## Best Practices and Pythonic Code

```python
# 1. Use list comprehensions instead of loops for building lists
# Not Pythonic
squares = []
for x in range(10):
    squares.append(x**2)

# Pythonic
squares = [x**2 for x in range(10)]

# 2. Use enumerate instead of range(len())
# Not Pythonic
for i in range(len(fruits)):
    print(i, fruits[i])

# Pythonic
for i, fruit in enumerate(fruits):
    print(i, fruit)

# 3. Use zip instead of index tricks to iterate two lists together
for name, score in zip(names, scores):
    print(name, score)

# 4. Use dict.get() for safe access
user.get("name", "Unknown")   # instead of user["name"] which can crash

# 5. Use "in" for membership checks
if name in valid_names:   # O(1) for sets/dicts, O(n) for lists
    pass

# 6. Use f-strings for formatting
name = f"Hello, {name}!"   # not "Hello, " + name + "!"

# 7. Use truthiness directly
if items:           # not "if len(items) > 0:"
    pass

if not items:       # not "if len(items) == 0:"
    pass

if user is None:    # check None explicitly
    pass

# 8. Use _ for unused variables
for _ in range(5):  # you do not need the loop variable
    do_something()

first, _, last = (1, 2, 3)  # ignore the middle value

# 9. Use context managers for resource management
with open("file.txt") as f:   # not open/try/finally/close
    data = f.read()

# 10. Prefer exceptions over checking first (EAFP style)
# Not Pythonic (LBYL: Look Before You Leap)
if key in dictionary:
    value = dictionary[key]

# Pythonic (EAFP: Easier to Ask Forgiveness than Permission)
try:
    value = dictionary[key]
except KeyError:
    value = default

# 11. Use @property for computed attributes
class Circle:
    def __init__(self, radius):
        self.radius = radius

    @property
    def area(self):
        return math.pi * self.radius ** 2

# 12. Keep functions small and focused (single responsibility)
# 13. Follow PEP 8 style guide: snake_case for variables/functions, PascalCase for classes
# 14. Write docstrings for all public functions and classes
# 15. Use virtual environments for every project (venv, conda)
```

---

## Common Interview Questions

### Q1. What is Python and what are its main features?
Python is a high-level, interpreted, dynamically typed, general-purpose language focused on readability and simplicity. Its key features are clean, readable syntax that looks almost like English, a massive standard library, dynamic typing so you do not declare types, automatic memory management through garbage collection, and being multi-paradigm so you can write procedural, object-oriented, or functional code.

### Q2. What is the difference between a list and a tuple?
A list is mutable (you can add, remove, and change items) and is created with square brackets. A tuple is immutable (once created, it cannot be changed) and is created with parentheses. Because tuples are immutable, they are faster, can be used as dictionary keys, and can be stored in sets. Use tuples for data that should not change, like coordinates or RGB values, and lists for data you need to modify.

### Q3. What is the GIL in Python?
The GIL (Global Interpreter Lock) is a mutex inside CPython (the default Python interpreter) that ensures only one thread executes Python bytecode at a time, even on a multi-core machine. This means Python threads cannot truly run in parallel for CPU-bound tasks. The practical consequence is: use `threading` or `asyncio` for I/O-bound tasks (network calls, file I/O, where threads spend time waiting), and use `multiprocessing` for CPU-bound tasks (since each process has its own GIL and runs on its own core).

### Q4. What is the difference between `is` and `==`?
`==` checks if two values are equal in terms of content. `is` checks if two variables point to the exact same object in memory (same identity). So two different lists with the same content will be `==` True but `is` False. Only use `is` when checking against `None`, `True`, or `False`, because for other objects it can give surprising results due to Python's internal object caching and interning.

### Q5. How do decorators work in Python?
A decorator is a function that takes another function as input and returns a new, enhanced version of it. When you write `@my_decorator` above a function, Python automatically passes that function to `my_decorator` and replaces it with whatever `my_decorator` returns. Decorators are used for adding cross-cutting concerns like logging, authentication, caching, and timing without modifying the original function's code.

### Q6. What is the difference between `*args` and `**kwargs`?
`*args` collects any extra positional arguments passed to a function into a tuple. `**kwargs` collects any extra keyword arguments into a dictionary. Both let you write flexible functions that accept any number of arguments. The names `args` and `kwargs` are just conventions, the `*` and `**` are what actually matter.

### Q7. What are generators and why are they useful?
A generator is a function that uses `yield` instead of `return` to produce a sequence of values one at a time, pausing between each value. Unlike a list that loads all items into memory at once, a generator produces each value on demand (lazily), which makes it extremely memory-efficient for working with large datasets. You can iterate over a generator with a for loop or call `next()` on it.

### Q8. What is the difference between `deepcopy` and a shallow copy?
A shallow copy creates a new container object but fills it with references to the same inner objects as the original. So if the inner objects are mutable (like lists), changing them in the copy also changes them in the original. A deep copy recursively creates completely new copies of everything, including all nested objects. Use `list.copy()` or `[:]` for shallow copy and `copy.deepcopy()` for a complete independent copy.

### Q9. What are Python's mutable and immutable types?
Immutable types cannot be changed after creation: integers, floats, strings, tuples, booleans, and frozensets. Mutable types can be changed in place: lists, dictionaries, sets, and most custom class instances. This distinction matters because mutable objects should not be used as default function arguments (they are shared across all calls) and only immutable objects can be used as dictionary keys or stored in sets.

### Q10. What is a context manager and why would you use one?
A context manager is an object that defines what should happen when you enter and exit a `with` block, through `__enter__` and `__exit__` methods. The most common use is ensuring a resource is properly cleaned up even if an exception occurs, like automatically closing a file, releasing a database connection, or releasing a threading lock. You can create your own using a class with `__enter__`/`__exit__` or by using the `@contextmanager` decorator from `contextlib`.

### Q11. What is the difference between a class method, a static method, and an instance method?
An instance method receives `self` as the first argument and can access and modify the instance's data. A class method is decorated with `@classmethod` and receives `cls` as the first argument, giving it access to the class itself rather than an instance, commonly used as alternative constructors. A static method is decorated with `@staticmethod` and receives no automatic first argument, so it has no access to the instance or the class, making it essentially just a regular function that lives inside the class for organizational purposes.

### Q12. What is a list comprehension and why is it Pythonic?
A list comprehension is a concise, single-line way to create a list by applying an expression to each item of an iterable, optionally filtering with a condition. For example, `[x**2 for x in range(10) if x % 2 == 0]`. It is considered Pythonic because it is typically more readable and faster than an equivalent for loop with `append()`. Python also has dictionary, set, and generator comprehensions using the same syntax.

### Q13. What is multiple inheritance and what is MRO?
Multiple inheritance means a class can inherit from more than one parent class, getting attributes and methods from all of them. MRO (Method Resolution Order) is the order in which Python searches through the classes to find a method when it is called. Python uses the C3 linearization algorithm to determine this order, and you can inspect it with `ClassName.__mro__`. The common problem is the "diamond problem" (two parents share a common grandparent) which Python's MRO handles correctly.

### Q14. How does memory management work in Python?
Python manages memory through reference counting as the primary mechanism. Every object keeps a count of how many variables reference it, and when that count drops to zero the memory is freed immediately. For cases where reference counting cannot work, like circular references (object A points to B, B points back to A), Python has a cyclic garbage collector that periodically finds and cleans these up. The `gc` module lets you control this. There is also a memory pool (pymalloc) for small objects to reduce allocation overhead.

### Q15. What is the difference between `__str__` and `__repr__`?
Both return a string representation of an object. `__str__` is meant to be readable and user-friendly, used by `print()` and `str()`. `__repr__` is meant to be unambiguous and developer-friendly, ideally returning a string that could recreate the object with `eval()`, used in the REPL and by `repr()`. If you only define one, define `__repr__` because Python falls back to it when `__str__` is missing. A good rule is: `__str__` is for users, `__repr__` is for developers debugging.

---

## Contributing

Found a mistake or want to add something? Open a PR or raise an issue. All contributions are welcome.

---

## Author

**Haseeb Javed**
Full-Stack Developer | React, Next.js, TypeScript, NestJS, Django, FastAPI

- GitHub: [@haseebjaved4212](https://github.com/haseebjaved4212)
- Email: contactimhaseeb@gmail.com

---

## License

This project is open source and available under the [MIT License](LICENSE).