# Python Basics

This tutorial covers the fundamental Python concepts you need for data analysis.

## Python as a Calculator

Python can perform arithmetic operations:

```python
# Basic operations
print(2 + 3)        # Addition: 5
print(10 - 4)       # Subtraction: 6
print(5 * 6)        # Multiplication: 30
print(20 / 4)       # Division: 5.0
print(7 // 2)       # Integer division: 3
print(7 % 2)        # Modulo (remainder): 1
print(2 ** 3)       # Exponentiation: 8
```

## Variables

Variables store values for later use:

```python
# Assign values to variables
name = "Alice"
age = 30
height = 5.6
is_analyst = True

# Use variables
print(f"{name} is {age} years old")
```

### Variable Naming Rules

- ✅ Use letters, numbers, and underscores
- ✅ Start with a letter or underscore
- ✅ Use descriptive names: `total_sales` not `ts`
- ❌ Don't use Python keywords: `for`, `if`, `class`
- ❌ Don't start with numbers

## Data Types

### Common Types

```python
# Integer
count = 42
print(type(count))  # <class 'int'>

# Float (decimal)
price = 19.99
print(type(price))  # <class 'float'>

# String (text)
message = "Hello, World!"
print(type(message))  # <class 'str'>

# Boolean (True/False)
is_valid = True
print(type(is_valid))  # <class 'bool'>

# None (absence of value)
result = None
print(type(result))  # <class 'NoneType'>
```

## Lists

Lists store multiple values in order:

```python
# Create a list
numbers = [1, 2, 3, 4, 5]
names = ["Alice", "Bob", "Charlie"]
mixed = [1, "two", 3.0, True]

# Access elements (0-based indexing!)
print(numbers[0])    # First element: 1
print(numbers[-1])   # Last element: 5

# Slicing
print(numbers[1:3])  # Elements 1-2: [2, 3]
print(numbers[:2])   # First 2: [1, 2]
print(numbers[2:])   # From index 2: [3, 4, 5]

# Modify lists
numbers.append(6)           # Add to end
numbers.insert(0, 0)        # Insert at position
numbers.remove(3)           # Remove value
popped = numbers.pop()      # Remove and return last

# List operations
print(len(numbers))         # Length
print(sum(numbers))         # Sum
print(max(numbers))         # Maximum
```

## Dictionaries

Dictionaries store key-value pairs:

```python
# Create a dictionary
person = {
    "name": "Alice",
    "age": 30,
    "department": "Sales"
}

# Access values
print(person["name"])              # Alice
print(person.get("age"))           # 30
print(person.get("salary", 0))     # 0 (default if missing)

# Modify dictionaries
person["age"] = 31                 # Update value
person["salary"] = 50000           # Add new key
del person["department"]           # Delete key

# Dictionary operations
print(person.keys())               # All keys
print(person.values())             # All values
print(person.items())              # Key-value pairs
```

## Control Flow

### If Statements

```python
age = 25

if age < 18:
    print("Minor")
elif age < 65:
    print("Adult")
else:
    print("Senior")

# Conditional expressions
status = "Adult" if age >= 18 else "Minor"
```

### For Loops

```python
# Loop over a list
names = ["Alice", "Bob", "Charlie"]
for name in names:
    print(f"Hello, {name}!")

# Loop over a range
for i in range(5):
    print(i)  # 0, 1, 2, 3, 4

# Loop with index
for i, name in enumerate(names):
    print(f"{i}: {name}")
```

### While Loops

```python
count = 0
while count < 5:
    print(count)
    count += 1
```

## Functions

Functions organize reusable code:

```python
# Define a function
def greet(name):
    return f"Hello, {name}!"

# Call the function
message = greet("Alice")
print(message)

# Multiple parameters
def calculate_total(price, quantity, tax_rate=0.1):
    subtotal = price * quantity
    tax = subtotal * tax_rate
    total = subtotal + tax
    return total

# Call with positional and keyword arguments
total = calculate_total(19.99, 3, tax_rate=0.08)
print(f"Total: ${total:.2f}")
```

## List Comprehensions

A concise way to create lists:

```python
# Traditional way
squares = []
for i in range(10):
    squares.append(i ** 2)

# List comprehension
squares = [i ** 2 for i in range(10)]

# With condition
even_squares = [i ** 2 for i in range(10) if i % 2 == 0]

# Transform data
names = ["alice", "bob", "charlie"]
upper_names = [name.upper() for name in names]
```

## Working with Strings

```python
text = "  Python for Data Analysis  "

# String methods
print(text.strip())           # Remove whitespace
print(text.lower())           # Lowercase
print(text.upper())           # Uppercase
print(text.replace("Python", "R"))  # Replace

# String formatting
name = "Alice"
age = 30
print(f"{name} is {age} years old")  # f-strings (recommended)
print("{} is {} years old".format(name, age))  # format method
print("%s is %d years old" % (name, age))      # old style

# String operations
print("Data" + " " + "Science")   # Concatenation
print("Python " * 3)              # Repetition
print("ana" in "banana")          # Membership: True
```

## Importing Modules

Python's power comes from its libraries:

```python
# Import entire module
import math
print(math.sqrt(16))

# Import specific functions
from math import sqrt, pi
print(sqrt(16))
print(pi)

# Import with alias
import pandas as pd
import numpy as np

# Common data analysis imports
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

## Error Handling

```python
# Try-except block
try:
    result = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero!")
    result = None

# Multiple exceptions
try:
    value = int("not a number")
except ValueError:
    print("Invalid number format")
except Exception as e:
    print(f"An error occurred: {e}")

# Finally clause (always executes)
try:
    file = open("data.csv")
    # process file
except FileNotFoundError:
    print("File not found")
finally:
    file.close()  # Always close the file
```

## File Operations

```python
# Read a file
with open("data.txt", "r") as file:
    content = file.read()
    print(content)

# Read line by line
with open("data.txt", "r") as file:
    for line in file:
        print(line.strip())

# Write to a file
with open("output.txt", "w") as file:
    file.write("Hello, World!\n")
    file.write("Python is great!\n")

# Append to a file
with open("output.txt", "a") as file:
    file.write("Appended line\n")
```

## Best Practices

!!! tip "Use meaningful variable names"
    ```python
    # Good
    total_sales = 1000
    customer_count = 50
    
    # Bad
    ts = 1000
    n = 50
    ```

!!! tip "Follow PEP 8 style guide"
    - Use 4 spaces for indentation
    - Use `snake_case` for variables and functions
    - Use `CamelCase` for class names
    - Limit lines to 79 characters

!!! tip "Comment your code"
    ```python
    # Calculate the average
    average = sum(values) / len(values)
    ```

!!! warning "Watch out for indentation"
    Python uses indentation to define code blocks. Mixing tabs and spaces causes errors!

## Practice Exercises

Try these on your own:

1. Create a list of numbers and calculate their average
2. Write a function that checks if a number is prime
3. Use a dictionary to count word frequencies in a sentence
4. Create a list comprehension to filter even numbers
5. Write a program that reads a CSV file line by line

## Next Steps

- Continue to [Pandas Fundamentals](02-pandas-fundamentals.md)
- Practice in `notebooks/01-introduction.ipynb`
- Try the interactive Python tutorial at [python.org/about/gettingstarted](https://www.python.org/about/gettingstarted/)

You now have the Python foundation needed for data analysis!
