# Quick Start Guide

Your first steps with Python for data analysis. This guide assumes you've completed the [Installation Guide](installation.md).

## Before You Begin

Make sure you have:

- ✅ Python and Git installed
- ✅ Virtual environment created and activated
- ✅ VS Code set up with Jupyter extension
- ✅ Repository cloned

If not, see the [Installation Guide](installation.md).

## Your First Data Analysis

### Open VS Code

1. Launch VS Code
2. `File > Open Folder` → select `Data-Wizardry-with-Python`
3. Select your Python interpreter (`Ctrl+Shift+P` → "Python: Select Interpreter" → choose `.venv`)

### Create Your First Notebook

1. In Explorer, right-click the `notebooks/` folder
2. Select **New File**
3. Name it `my_first_analysis.ipynb`
4. The notebook opens in VS Code

### **Cell 1** - Import libraries

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Display settings
pd.options.display.max_columns = 50
pd.options.display.width = 120

print("✓ Libraries loaded successfully!")
```

Run the cell with `Shift+Enter`. You should see the success message.

**Cell 2** - Load the sample data:

```python
# Load demographic data
df = pd.read_csv('data/socio_demos.csv')

# Quick look at the data
df.head()
```

**Cell 3** - Explore the data structure:

**Cell 1** - Import libraries:

**Cell 3** - Explore the data structure:

```python
# Shape and info
print(f"Rows: {df.shape[0]}, Columns: {df.shape[1]}")
print("\nColumn types:")
print(df.dtypes)
print("\nMissing values:")
print(df.isnull().sum())
```

**Cell 4** - Basic statistics:

```python
# Summary statistics
df.describe()
```

**Cell 5** - Create a simple visualization:

```python
# Example: visualize a distribution (adjust column name as needed)
df.select_dtypes(include=[np.number]).iloc[:, 0].hist(bins=20, figsize=(8, 4))
plt.title('Distribution of First Numeric Column')
plt.xlabel('Value')
plt.ylabel('Frequency')
plt.tight_layout()
plt.show()
```

Congratulations! You've just completed your first data analysis in Python.

## Essential pandas Operations

### Selecting Data

```python
# Select a single column
df['column_name']

# Select multiple columns
df[['col1', 'col2', 'col3']]

# Select rows by condition
df[df['age'] > 30]

# Select rows and columns together
df.loc[df['age'] > 30, ['name', 'age', 'department']]
```

### Filtering and Sorting

```python
# Filter rows
young_employees = df[df['age'] < 30]

# Multiple conditions (use & for AND, | for OR)
filtered = df[(df['age'] > 25) & (df['department'] == 'Sales')]

# Sort by column
df.sort_values('age', ascending=False)

# Sort by multiple columns
df.sort_values(['department', 'age'])
```

### Grouping and Aggregating

```python
# Group by one column
df.groupby('department')['salary'].mean()

# Group by multiple columns
df.groupby(['department', 'location'])['salary'].agg(['mean', 'count'])

# Multiple aggregations
df.groupby('department').agg({
    'salary': ['mean', 'min', 'max'],
    'age': 'mean'
})
```

### Creating New Columns

```python
# Simple calculation
df['bonus'] = df['salary'] * 0.10

# Conditional column
df['category'] = df['age'].apply(lambda x: 'Senior' if x > 40 else 'Junior')

# Using np.where for conditions
df['status'] = np.where(df['salary'] > 60000, 'High', 'Standard')
```

## Working with Real Data

### Load Your Own Data

```python
# CSV file
df = pd.read_csv('path/to/your_file.csv')

# Excel file
df = pd.read_excel('path/to/your_file.xlsx', sheet_name='Sheet1')

# Specify encoding if needed
df = pd.read_csv('file.csv', encoding='utf-8')

# Skip rows or specify column names
df = pd.read_csv('file.csv', skiprows=2, names=['col1', 'col2', 'col3'])
```

### Handle Missing Data

```python
# Check for missing values
df.isnull().sum()

# Drop rows with any missing values
df_clean = df.dropna()

# Drop rows where specific column is missing
df_clean = df.dropna(subset=['important_column'])

# Fill missing values
df['column'].fillna(0, inplace=True)  # With a value
df['column'].fillna(df['column'].mean(), inplace=True)  # With mean
```

### Export Results

```python
# Save to CSV
df.to_csv('output.csv', index=False)

# Save to Excel
df.to_excel('output.xlsx', sheet_name='Results', index=False)

# Save specific columns
df[['col1', 'col2']].to_csv('subset.csv', index=False)
```

## Common Tasks Cheat Sheet

| Task | Code |
|------|------|
| Load CSV | `pd.read_csv('file.csv')` |
| First 5 rows | `df.head()` |
| Last 5 rows | `df.tail()` |
| Shape (rows, cols) | `df.shape` |
| Column names | `df.columns` |
| Data types | `df.dtypes` |
| Summary stats | `df.describe()` |
| Missing values | `df.isnull().sum()` |
| Unique values | `df['col'].unique()` |
| Value counts | `df['col'].value_counts()` |
| Filter rows | `df[df['col'] > 10]` |
| Sort | `df.sort_values('col')` |
| Group by | `df.groupby('col').mean()` |
| New column | `df['new'] = df['a'] + df['b']` |
| Drop column | `df.drop('col', axis=1)` |
| Save to CSV | `df.to_csv('out.csv', index=False)` |

## Getting Help

### In Your Notebook

```python
# Quick help on any function
pd.read_csv?

# Detailed help
help(pd.DataFrame)

# See all methods of an object
dir(df)
```

### Keyboard Shortcuts (VS Code)

- `Shift+Enter`: Run cell and move to next
- `Ctrl+Enter`: Run cell and stay
- `Esc then A`: Insert cell above
- `Esc then B`: Insert cell below
- `Esc then DD`: Delete cell
- `Esc then M`: Convert to Markdown
- `Esc then Y`: Convert to Code

## Next Steps

Now that you've got the basics:

1. **Explore the notebooks**: Try `notebooks/01_data_loading.ipynb`
2. **Learn Python basics**: Read [Python Basics for Analysts](../guides/python_basics_for_analysts.md)
3. **Master pandas**: Check out the [Pandas Overview](../guides/pandas/overview.md)
4. **Coming from R?**: See the [R to Python Guide](r-to-python.md)
5. **Coming from SPSS?**: See the [SPSS to Python Guide](spss-to-python.md)

## Tips for Success

1. **Experiment**: Try modifying the code examples
2. **Use Markdown cells**: Document your thought process
3. **Save often**: `Ctrl+S` to save your notebook
4. **Restart kernel**: If things get weird, restart the kernel (`Ctrl+Shift+P` → "Jupyter: Restart Kernel")
5. **Check data types**: Many errors come from unexpected data types
6. **Read error messages**: They usually point to the problem

Happy analyzing! 🎉
