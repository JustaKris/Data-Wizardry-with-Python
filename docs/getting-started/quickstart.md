# Quick Start Guide

Let's write your first Python code for data analysis! This guide will get you comfortable with the basics in just a few minutes.

## Your First Python Session

### Using Jupyter in VS Code (Recommended)

VS Code provides the best integrated experience for working with Jupyter notebooks.

1. **Open VS Code** and open the project folder:
   - `File > Open Folder`
   - Select `Data-Wizardry-with-Python`

2. **Select your Python interpreter**:
   - Press `Ctrl+Shift+P` (or `Cmd+Shift+P` on Mac)
   - Type "Python: Select Interpreter"
   - Choose your virtual environment (`.venv` or `venv`)

3. **Open or create a notebook**:
   - In the Explorer panel, navigate to `notebooks/`
   - Click `01-introduction.ipynb` to open it
   - Or create a new one: Right-click in Explorer → `New File` → name it with `.ipynb` extension

4. **Write your first code**:
   In the first cell, type:
   
   ```python
   print("Hello, Python Analytics!")
   ```

5. **Run it**:
   - Click the play (▶) button next to the cell
   - Or press `Shift + Enter`

You should see the output appear below the cell!

**VS Code Jupyter Tips:**
- IntelliSense provides auto-completion as you type
- Hover over variables to see their values
- Use the Variable Explorer in the top toolbar
- Integrated debugging available with breakpoints

### Using Jupyter Lab (Browser-Based Alternative)

If you prefer the traditional browser interface:

1. Open your terminal in VS Code (`Ctrl+` ` or `Terminal > New Terminal`)

2. Start Jupyter Lab:

   ```bash
   jupyter lab
   ```

3. Your browser will open to Jupyter Lab

4. Create a new notebook:
   - Click "Python 3" under "Notebook"
   - You'll see an empty cell

5. Type this code and press `Shift + Enter`:

   ```python
   print("Hello, Python Analytics!")
   ```

## Loading Data with pandas

Let's load and explore a dataset. In a new cell:

```python
import pandas as pd
import numpy as np

# Create a sample dataset
data = {
    'Name': ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve'],
    'Age': [25, 30, 35, 28, 32],
    'Department': ['Sales', 'IT', 'Sales', 'HR', 'IT'],
    'Salary': [50000, 60000, 55000, 52000, 65000]
}

df = pd.DataFrame(data)
print(df)
```

**Output:**

```text
      Name  Age Department  Salary
0    Alice   25      Sales   50000
1      Bob   30         IT   60000
2  Charlie   35      Sales   55000
3    Diana   28         HR   52000
4      Eve   32         IT   65000
```

## Basic Data Exploration

Try these operations in separate cells:

### View first rows

```python
df.head()
```

### Get summary statistics

```python
df.describe()
```

### Check data types

```python
df.dtypes
```

### Filter data

```python
# Get all employees in Sales
sales_team = df[df['Department'] == 'Sales']
print(sales_team)
```

### Calculate averages

```python
# Average salary by department
avg_salary = df.groupby('Department')['Salary'].mean()
print(avg_salary)
```

## Creating a Simple Plot

```python
import matplotlib.pyplot as plt

# Create a bar chart of average salary by department
avg_salary.plot(kind='bar', color='skyblue')
plt.title('Average Salary by Department')
plt.xlabel('Department')
plt.ylabel('Average Salary ($)')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```

## Common Operations Cheat Sheet

| Task | Code |
|------|------|
| Import pandas | `import pandas as pd` |
| Read CSV | `df = pd.read_csv('file.csv')` |
| Read Excel | `df = pd.read_excel('file.xlsx')` |
| View data | `df.head()` or `df.tail()` |
| Get shape | `df.shape` |
| Column names | `df.columns` |
| Select column | `df['column_name']` |
| Filter rows | `df[df['col'] > 10]` |
| Sort | `df.sort_values('column')` |
| Group by | `df.groupby('column').mean()` |

## Next Steps

!!! success "Congratulations!"
    You've just performed your first data analysis in Python!

Now you can:

- **Coming from R?** → [R to Python Guide](r-to-python.md)
- **Coming from SPSS?** → [SPSS to Python Guide](spss-to-python.md)
- **Want to learn more?** → [Python Basics Tutorial](../tutorials/01-python-basics.md)
- **Ready to practice?** → Open `notebooks/01-introduction.ipynb`

## Helpful Tips

### Jupyter Keyboard Shortcuts

- `Shift + Enter`: Run cell and move to next
- `Ctrl + Enter`: Run cell and stay on it
- `Esc`: Enter command mode
- `A`: Insert cell above
- `B`: Insert cell below
- `DD`: Delete cell
- `M`: Convert to Markdown
- `Y`: Convert to Code

### Getting Help

In Jupyter, you can get help on any function:

```python
# Add a question mark
pd.read_csv?

# Or use help()
help(pd.DataFrame)
```

### Best Practices

1. **Use meaningful variable names**: `sales_data` not `df1`
2. **Comment your code**: Explain what and why
3. **Keep cells small**: One concept per cell
4. **Save frequently**: Don't lose your work!

Happy coding! 🎉
