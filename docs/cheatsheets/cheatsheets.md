# Cheat Sheets

Quick reference guides for common Python data analysis operations.

## Core Libraries

### pandas

For comprehensive pandas reference, see our dedicated pandas guides:

- **[pandas Overview](../guides/pandas/overview.md)** - Complete guide to pandas
- **[pandas Cheat Sheet](../guides/pandas/cheat_sheet.md)** - Quick reference

## Python Basics

### Common Data Types

```python
42              # int
3.14            # float
"text"          # str
True/False      # bool
[1, 2, 3]       # list (mutable)
(1, 2, 3)       # tuple (immutable)
{'a': 1, 'b': 2}  # dict
{1, 2, 3}       # set
```

### Control Structures

```python
# Conditional
if condition:
    # do something
elif other_condition:
    # do something else
else:
    # default

# For loop
for item in items:
    print(item)

# While loop
while condition:
    # repeat

# List comprehension
squares = [x**2 for x in range(10)]
evens = [x for x in range(10) if x % 2 == 0]

# Dict comprehension
{k: v**2 for k, v in dict.items()}
```

### Function Definitions

```python
def function_name(param1, param2='default'):
    """Docstring describing the function."""
    result = param1 + param2
    return result

# Lambda (anonymous function)
square = lambda x: x**2

# Multiple return values
def min_max(numbers):
    return min(numbers), max(numbers)
```

### String Operations

```python
# Formatting (use f-strings in modern Python)
name, age = "Alice", 25
f"Hello, {name}! You are {age} years old."
f"Result: {value:.2f}"  # Format with 2 decimals

# Common methods
text.lower()            # Lowercase
text.upper()            # Uppercase
text.strip()            # Remove whitespace
text.replace('old', 'new')
text.split(',')         # Split into list
','.join(items)         # Join list into string
'substring' in text     # Check contains
```

## matplotlib

### Basic Plotting

```python
import matplotlib.pyplot as plt

# Line plot
plt.plot(x, y)
plt.plot(x, y, label='Series 1', color='blue', linestyle='--')

# Customize
plt.xlabel('X Label')
plt.ylabel('Y Label')
plt.title('Title')
plt.legend()
plt.grid(True)
plt.tight_layout()
plt.show()

# Save figure
plt.savefig('plot.png', dpi=300, bbox_inches='tight')
```

### Common Plot Types

```python
plt.scatter(x, y)               # Scatter plot
plt.bar(categories, values)     # Bar chart
plt.barh(categories, values)    # Horizontal bar chart
plt.hist(data, bins=20)         # Histogram
plt.boxplot(data)               # Box plot
plt.pie(sizes, labels=labels)   # Pie chart

# Subplots
fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(10, 4))
ax1.plot(x, y1)
ax2.scatter(x, y2)
```

## seaborn

### Statistical Plotting

```python
import seaborn as sns

# Set style
sns.set_theme(style='whitegrid')
sns.set_palette('husl')

# Distribution plots
sns.histplot(data=df, x='value', bins=20)
sns.kdeplot(data=df, x='value')
sns.boxplot(data=df, x='category', y='value')
sns.violinplot(data=df, x='category', y='value')

# Relationship plots
sns.scatterplot(data=df, x='x', y='y', hue='category')
sns.lineplot(data=df, x='time', y='value', hue='group')
sns.regplot(data=df, x='x', y='y')  # With regression line

# Categorical plots
sns.barplot(data=df, x='category', y='value')
sns.countplot(data=df, x='category')

# Matrix plots
sns.heatmap(df.corr(), annot=True, cmap='coolwarm')
sns.clustermap(df, cmap='viridis')
```

## NumPy

### Array Creation

```python
import numpy as np

# From Python objects
np.array([1, 2, 3])
np.array([[1, 2], [3, 4]])

# Initialized arrays
np.zeros(5)                  # All zeros
np.ones((3, 3))              # All ones
np.full((2, 2), 7)           # All 7s
np.eye(3)                    # Identity matrix

# Ranges
np.arange(0, 10, 2)          # [0, 2, 4, 6, 8]
np.linspace(0, 1, 5)         # 5 values from 0 to 1

# Random
np.random.rand(3, 3)         # Uniform [0, 1)
np.random.randn(3, 3)        # Standard normal
np.random.randint(0, 10, 5)  # Random integers
```

### Array Operations

```python
# Math operations (element-wise)
arr + 5
arr * 2
arr ** 2
np.sqrt(arr)
np.exp(arr)
np.log(arr)

# Aggregations
arr.mean()
arr.std()
arr.min()
arr.max()
arr.sum()
arr.cumsum()

# Axis operations
arr.mean(axis=0)  # Column means
arr.sum(axis=1)   # Row sums

# Reshaping
arr.reshape(3, 4)
arr.flatten()
arr.T  # Transpose
```

## scipy.stats

### Statistical Tests

```python
from scipy import stats

# T-tests
stats.ttest_1samp(data, popmean=0)           # One-sample
stats.ttest_ind(group1, group2)               # Independent samples
stats.ttest_rel(before, after)                # Paired samples

# Correlation
stats.pearsonr(x, y)                          # Pearson correlation
stats.spearmanr(x, y)                         # Spearman correlation

# ANOVA
stats.f_oneway(group1, group2, group3)        # One-way ANOVA

# Chi-square
stats.chi2_contingency(crosstab)              # Chi-square test

# Normality tests
stats.shapiro(data)                           # Shapiro-Wilk test
stats.normaltest(data)                        # D'Agostino-Pearson test

# Non-parametric
stats.mannwhitneyu(group1, group2)            # Mann-Whitney U
stats.wilcoxon(before, after)                 # Wilcoxon signed-rank
stats.kruskal(group1, group2, group3)         # Kruskal-Wallis
```

### Distributions

```python
# Normal distribution
stats.norm.pdf(x, loc=0, scale=1)             # Probability density
stats.norm.cdf(x, loc=0, scale=1)             # Cumulative distribution
stats.norm.ppf(0.95, loc=0, scale=1)          # Quantile (inverse CDF)
stats.norm.rvs(loc=0, scale=1, size=100)      # Random samples
```

## Jupyter Keyboard Shortcuts

### Command Mode (press Esc to enter)

| Shortcut | Action |
|----------|--------|
| `A` | Insert cell above |
| `B` | Insert cell below |
| `DD` | Delete cell |
| `M` | Convert to Markdown |
| `Y` | Convert to Code |
| `Z` | Undo delete cell |
| `Shift+J` | Select cells below |
| `Shift+K` | Select cells above |
| `Shift+M` | Merge selected cells |

### Edit Mode (press Enter to enter)

| Shortcut | Action |
|----------|--------|
| `Shift+Enter` | Run cell, select below |
| `Ctrl+Enter` | Run cell |
| `Alt+Enter` | Run cell, insert below |
| `Ctrl+/` | Comment/uncomment |
| `Tab` | Indent or autocomplete |
| `Shift+Tab` | Show function tooltip |
| `Ctrl+]` | Indent |
| `Ctrl+[` | Dedent |

## Common Workflows

### Data Loading Pipeline

```python
import pandas as pd
import numpy as np

# Load data
df = pd.read_csv('data.csv')

# Initial inspection
print(df.shape)
print(df.head())
print(df.info())

# Check missing values
print(df.isnull().sum())

# Summary statistics
print(df.describe())
```

### Data Cleaning Pipeline

```python
# Remove duplicates
df = df.drop_duplicates()

# Handle missing values
df = df.dropna(subset=['important_col'])
df['col'].fillna(df['col'].mean(), inplace=True)

# Fix data types
df['date'] = pd.to_datetime(df['date'])
df['category'] = df['category'].astype('category')

# Remove outliers (example: remove values > 3 std dev)
df = df[np.abs(df['value'] - df['value'].mean()) <= (3 * df['value'].std())]
```

### Analysis and Visualization

```python
import matplotlib.pyplot as plt
import seaborn as sns

# Group and aggregate
summary = df.groupby('category')['value'].agg(['mean', 'count', 'std'])

# Visualize
sns.barplot(data=df, x='category', y='value')
plt.title('Average Value by Category')
plt.tight_layout()
plt.show()

# Export results
summary.to_csv('summary.csv')
```

## External Resources

### Official Documentation

- **pandas**: [pandas.pydata.org/docs](https://pandas.pydata.org/docs/)
- **NumPy**: [numpy.org/doc](https://numpy.org/doc/)
- **Matplotlib**: [matplotlib.org](https://matplotlib.org/)
- **seaborn**: [seaborn.pydata.org](https://seaborn.pydata.org/)
- **SciPy**: [docs.scipy.org](https://docs.scipy.org/)

### Downloadable Cheat Sheets

- [pandas Official Cheat Sheet (PDF)](https://pandas.pydata.org/Pandas_Cheat_Sheet.pdf)
- [NumPy Cheat Sheet](https://numpy.org/doc/stable/user/absolute_beginners.html)
- [Matplotlib Cheat Sheets](https://matplotlib.org/cheatsheets/)
- [seaborn Tutorial](https://seaborn.pydata.org/tutorial.html)

### Quick Tutorials

- **pandas**: [10 Minutes to pandas](https://pandas.pydata.org/docs/user_guide/10min.html)
- **NumPy**: [NumPy Quickstart](https://numpy.org/doc/stable/user/quickstart.html)
- **Matplotlib**: [pyplot Tutorial](https://matplotlib.org/stable/tutorials/introductory/pyplot.html)
