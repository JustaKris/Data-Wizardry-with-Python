# Python Basics for Analysts

A practical guide to Python fundamentals for analysts transitioning from R or SPSS. This guide focuses on concepts relevant to data analysis work.

## Why Python for Data Analysis?

- **Versatile**: Data analysis, automation, web apps, machine learning
- **Large ecosystem**: pandas, NumPy, scikit-learn, and thousands more packages
- **Industry standard**: Widely used in tech, finance, healthcare, research
- **Open source**: Free, with excellent community support
- **Readable**: Clear syntax that's easy to learn and maintain

## Python Syntax Essentials

### Variables and Assignment

```python
# No need to declare types - Python infers them
name = "Alice"          # string
age = 25                # integer
height = 1.65           # float
is_analyst = True       # boolean

# Multiple assignment
x, y, z = 1, 2, 3

# Update variable
count = 0
count = count + 1  # or count += 1
```

### Comments

```python
# Single-line comment

"""
Multi-line comment
or docstring
"""

x = 5  # Inline comment
```

### Printing Output

```python
print("Hello, world!")
print(f"Name: {name}, Age: {age}")  # f-string (recommended)
print("Value:", 42, "Other:", 3.14)  # Multiple values
```

## Data Types for Analysts

### Numbers

```python
# Integers
count = 100
year = 2024

# Floats
price = 99.99
percentage = 0.15

# Operations
total = 10 + 5          # 15
difference = 10 - 5     # 5
product = 10 * 5        # 50
quotient = 10 / 5       # 2.0 (always float)
int_division = 10 // 3  # 3 (integer division)
remainder = 10 % 3      # 1 (modulo)
power = 2 ** 3          # 8

# Type conversion
int("42")               # String to int
float("3.14")           # String to float
str(42)                 # Int to string
```

### Strings

```python
# Creating strings
name = "Alice"
name = 'Alice'  # Single quotes work too
multiline = """This is
a multiline
string"""

# String operations
full_name = "Alice" + " " + "Smith"  # Concatenation
repeated = "Hi! " * 3                # "Hi! Hi! Hi! "

# Common methods
text = "  Hello World  "
text.lower()           # "  hello world  "
text.upper()           # "  HELLO WORLD  "
text.strip()           # "Hello World"
text.replace("Hello", "Hi")  # "  Hi World  "
text.split()           # ["Hello", "World"]

# String formatting (use f-strings!)
name = "Alice"
age = 25
message = f"Hello, {name}! You are {age} years old."
formatted = f"Price: ${price:.2f}"  # 2 decimal places
```

### Lists (Like Vectors/Arrays)

```python
# Creating lists
numbers = [1, 2, 3, 4, 5]
names = ["Alice", "Bob", "Charlie"]
mixed = [1, "two", 3.0, True]  # Can mix types

# Accessing elements (0-indexed!)
numbers[0]              # 1 (first element)
numbers[-1]             # 5 (last element)
numbers[1:3]            # [2, 3] (slicing, end exclusive)
numbers[:3]             # [1, 2, 3] (first 3)
numbers[2:]             # [3, 4, 5] (from index 2 on)

# Modifying
numbers[0] = 10         # Change element
numbers.append(6)       # Add to end
numbers.insert(0, 0)    # Insert at position
numbers.remove(3)       # Remove first occurrence
del numbers[0]          # Delete by index
numbers.pop()           # Remove and return last

# Common operations
len(numbers)            # Length
sum(numbers)            # Sum
min(numbers)            # Minimum
max(numbers)            # Maximum
sorted(numbers)         # Returns sorted copy
numbers.sort()          # Sort in place

# List comprehension (powerful!)
squares = [x**2 for x in range(1, 6)]  # [1, 4, 9, 16, 25]
evens = [x for x in numbers if x % 2 == 0]
```

### Dictionaries (Like Named Lists in R)

```python
# Creating dictionaries (key-value pairs)
person = {
    "name": "Alice",
    "age": 25,
    "city": "NYC"
}

# Accessing values
person["name"]          # "Alice"
person.get("age")       # 25
person.get("country", "USA")  # Default if key doesn't exist

# Modifying
person["age"] = 26      # Update value
person["email"] = "alice@example.com"  # Add new key
del person["city"]      # Remove key

# Common operations
person.keys()           # All keys
person.values()         # All values
person.items()          # Key-value pairs
"name" in person        # Check if key exists

# Iterating
for key in person:
    print(key, person[key])

for key, value in person.items():
    print(f"{key}: {value}")
```

### Booleans and Comparisons

```python
# Boolean values
is_valid = True
is_empty = False

# Comparisons
5 == 5              # True (equal)
5 != 3              # True (not equal)
5 > 3               # True (greater than)
5 >= 5              # True (greater or equal)
5 < 3               # False (less than)
5 <= 5              # True (less or equal)

# Logical operators
True and False      # False
True or False       # True
not True            # False

# Combining conditions
age = 25
if age >= 18 and age < 65:
    print("Working age")

# Check membership
"Alice" in ["Alice", "Bob"]  # True
"x" in "example"            # True
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

# Inline if (ternary operator)
status = "Adult" if age >= 18 else "Minor"

# Common patterns
if value is not None:
    # do something

if len(items) > 0:  # or just: if items:
    # process items
```

### For Loops

```python
# Loop over list
for name in ["Alice", "Bob", "Charlie"]:
    print(name)

# Loop over range
for i in range(5):          # 0, 1, 2, 3, 4
    print(i)

for i in range(1, 6):       # 1, 2, 3, 4, 5
    print(i)

for i in range(0, 10, 2):   # 0, 2, 4, 6, 8
    print(i)

# Loop with index
for i, name in enumerate(names):
    print(f"{i}: {name}")

# Loop over dictionary
for key, value in person.items():
    print(f"{key}: {value}")

# List comprehension (faster and more Pythonic)
squares = [x**2 for x in range(1, 6)]
filtered = [x for x in numbers if x > 10]
```

### While Loops

```python
count = 0
while count < 5:
    print(count)
    count += 1

# Break and continue
for i in range(10):
    if i == 3:
        continue  # Skip this iteration
    if i == 7:
        break     # Exit loop
    print(i)
```

## Functions

### Defining Functions

```python
def greet(name):
    """Print a greeting message."""
    print(f"Hello, {name}!")

greet("Alice")  # Call the function

# Return values
def add(a, b):
    """Return the sum of a and b."""
    return a + b

result = add(5, 3)  # 8

# Multiple return values
def min_max(numbers):
    """Return min and max of numbers."""
    return min(numbers), max(numbers)

minimum, maximum = min_max([1, 2, 3, 4, 5])

# Default parameters
def greet(name, greeting="Hello"):
    return f"{greeting}, {name}!"

greet("Alice")              # "Hello, Alice!"
greet("Bob", "Hi")          # "Hi, Bob!"

# Keyword arguments
def describe(name, age, city):
    return f"{name} is {age} years old and lives in {city}"

describe(name="Alice", age=25, city="NYC")  # Can specify in any order
```

### Lambda Functions

```python
# Anonymous functions (useful for quick operations)
square = lambda x: x**2
square(5)  # 25

# Often used with map, filter
numbers = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x**2, numbers))
evens = list(filter(lambda x: x % 2 == 0, numbers))

# But list comprehensions are often clearer
squared = [x**2 for x in numbers]
evens = [x for x in numbers if x % 2 == 0]
```

## Working with Files

### Reading Files

```python
# Read entire file
with open('data.txt', 'r') as file:
    content = file.read()

# Read line by line
with open('data.txt', 'r') as file:
    for line in file:
        print(line.strip())  # Remove newline

# Read into list
with open('data.txt', 'r') as file:
    lines = file.readlines()  # List of lines

# For CSV, use pandas!
import pandas as pd
df = pd.read_csv('data.csv')
```

### Writing Files

```python
# Write to file (overwrites)
with open('output.txt', 'w') as file:
    file.write("Hello, world!\n")
    file.write("Second line\n")

# Append to file
with open('output.txt', 'a') as file:
    file.write("Appended line\n")

# For CSV, use pandas!
df.to_csv('output.csv', index=False)
```

## Error Handling

```python
# Try-except blocks
try:
    result = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero!")

# Multiple exceptions
try:
    value = int(input("Enter a number: "))
    result = 10 / value
except ValueError:
    print("That's not a number!")
except ZeroDivisionError:
    print("Cannot divide by zero!")

# Catch all (use sparingly)
try:
    # risky operation
    pass
except Exception as e:
    print(f"Error: {e}")

# Finally block (always runs)
try:
    file = open('data.txt')
    # process file
finally:
    file.close()
```

## Importing Modules

### Standard Library

```python
# Import entire module
import math
math.sqrt(16)  # 4.0
math.pi        # 3.141592653589793

# Import specific items
from math import sqrt, pi
sqrt(16)  # No need for math.
pi

# Import with alias
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
```

### Organizing Code

```python
# my_functions.py
def calculate_total(prices):
    return sum(prices)

# main.py
from my_functions import calculate_total
total = calculate_total([10, 20, 30])
```

## Python for R Users

| Concept | R | Python (pandas) |
|---------|---|-----------------|
| Data frame | `df` | `df` |
| Select column | `df$column` or `df['column']` | `df['column']` |
| Filter rows | `df[df$age > 25, ]` | `df[df['age'] > 25]` |
| New column | `df$new <- df$a + df$b` | `df['new'] = df['a'] + df['b']` |
| Group by | `aggregate()` or `dplyr::group_by()` | `df.groupby().agg()` |
| Summary | `summary(df)` | `df.describe()` |
| Missing values | `is.na(df)` | `df.isnull()` |
| Join | `merge(df1, df2)` | `pd.merge(df1, df2)` |

## Python for SPSS Users

| Task | SPSS | Python (pandas) |
|------|------|-----------------|
| Import data | File → Open → Data | `pd.read_csv()` or `pd.read_spss()` |
| View data | Data View | `df.head()`, `df.info()` |
| Frequencies | Analyze → Descriptive → Frequencies | `df['col'].value_counts()` |
| Descriptives | Analyze → Descriptive → Descriptives | `df.describe()` |
| Filter | Data → Select Cases | `df[df['age'] > 25]` |
| Compute | Transform → Compute Variable | `df['new'] = df['a'] + df['b']` |
| Recode | Transform → Recode | `df['col'].replace()` or `df['col'].map()` |
| Cross-tabs | Analyze → Descriptive → Crosstabs | `pd.crosstab()` |
| T-test | Analyze → Compare Means → T-Test | `scipy.stats.ttest_ind()` |

## Best Practices

### Code Style

```python
# Use meaningful variable names
customer_age = 25  # Good
x = 25             # Bad

# Use snake_case for variables and functions
def calculate_total_price():
    pass

# Use UPPER_CASE for constants
MAX_RETRIES = 3
DEFAULT_TIMEOUT = 30

# Add docstrings to functions
def calculate_mean(values):
    """
    Calculate the mean of a list of values.
    
    Parameters:
    values (list): List of numeric values
    
    Returns:
    float: The mean value
    """
    return sum(values) / len(values)
```

### Common Pitfalls for Beginners

```python
# 1. Mutable default arguments (don't do this!)
def add_item(item, items=[]):  # BAD!
    items.append(item)
    return items

# Do this instead:
def add_item(item, items=None):
    if items is None:
        items = []
    items.append(item)
    return items

# 2. Integer division in Python 2 (not an issue in Python 3)
# Python 3: 5 / 2 = 2.5
# Python 2: 5 / 2 = 2 (use 5.0 / 2)

# 3. Modifying a list while iterating
# Don't do this:
for item in items:
    if condition:
        items.remove(item)  # BAD!

# Do this instead:
items = [item for item in items if not condition]

# 4. Using == to compare to None
# Don't: if x == None:
# Do: if x is None:
```

## Next Steps

Now that you know the basics:

1. **Practice with data**: Try the [Quick Start Guide](../getting-started/quickstart.md)
2. **Learn pandas**: See the [pandas Overview](pandas/overview.md)
3. **Explore notebooks**: Work through `notebooks/01_into_and_data_loading.ipynb`
4. **Cheat sheets**: Bookmark the [Cheat Sheets](../cheatsheets/cheatsheets.md)

## Recommended Learning Resources

- **Official Python Tutorial**: [docs.python.org/tutorial](https://docs.python.org/3/tutorial/)
- **Real Python**: [realpython.com](https://realpython.com/)
- **Python for Data Analysis** by Wes McKinney (pandas creator)
- **Automate the Boring Stuff with Python**: [automatetheboringstuff.com](https://automatetheboringstuff.com/)
