# Cheat Sheets

Quick reference guides for common operations.

## pandas Cheat Sheet

### Reading Data

```python
pd.read_csv('file.csv')
pd.read_excel('file.xlsx')
pd.read_spss('file.sav')
```

### Viewing Data

```python
df.head()           # First 5 rows
df.tail()           # Last 5 rows
df.shape            # (rows, cols)
df.info()           # Column info
df.describe()       # Statistics
```

### Selecting Data

```python
df['column']                    # Single column
df[['col1', 'col2']]           # Multiple columns
df.iloc[0]                      # First row by position
df.loc[0]                       # Row by index
df[df['age'] > 25]             # Filter rows
```

### Data Manipulation

```python
df['new'] = df['a'] + df['b']  # New column
df.drop('col', axis=1)          # Drop column
df.drop([0, 1])                 # Drop rows
df.sort_values('col')           # Sort
df.groupby('col').mean()        # Group and aggregate
```

### Missing Data

```python
df.isnull().sum()               # Count missing
df.dropna()                     # Drop rows with NaN
df.fillna(0)                    # Fill NaN with 0
```

### Merging Data

```python
pd.merge(df1, df2, on='id')    # Inner join
pd.concat([df1, df2])           # Concatenate
```

## matplotlib Cheat Sheet

### Basic Plot

```python
plt.plot(x, y)
plt.xlabel('X Label')
plt.ylabel('Y Label')
plt.title('Title')
plt.show()
```

### Common Plots

```python
plt.scatter(x, y)               # Scatter plot
plt.bar(categories, values)     # Bar chart
plt.hist(data, bins=20)         # Histogram
plt.boxplot(data)               # Box plot
```

## seaborn Cheat Sheet

### Statistical Plots

```python
sns.scatterplot(data=df, x='a', y='b')
sns.lineplot(data=df, x='x', y='y')
sns.barplot(data=df, x='cat', y='val')
sns.boxplot(data=df, x='cat', y='val')
sns.violinplot(data=df, x='cat', y='val')
sns.heatmap(df.corr(), annot=True)
```

## NumPy Cheat Sheet

### Array Creation

```python
np.array([1, 2, 3])            # From list
np.zeros(5)                     # All zeros
np.ones(5)                      # All ones
np.arange(0, 10, 2)            # Range
np.linspace(0, 1, 5)           # Evenly spaced
```

### Array Operations

```python
arr.mean()                      # Mean
arr.std()                       # Standard deviation
arr.min()                       # Minimum
arr.max()                       # Maximum
arr.sum()                       # Sum
```

## scipy.stats Cheat Sheet

### Statistical Tests

```python
stats.ttest_ind(group1, group2)         # t-test
stats.pearsonr(x, y)                    # Correlation
stats.chi2_contingency(crosstab)        # Chi-square test
stats.f_oneway(g1, g2, g3)             # One-way ANOVA
```

## Python Basics Cheat Sheet

### Data Types

```python
42              # int
3.14            # float
"text"          # str
True            # bool
[1, 2, 3]       # list
{'a': 1}        # dict
```

### Control Flow

```python
if condition:
    # do something
elif other_condition:
    # do something else
else:
    # default action

for item in items:
    # process item

while condition:
    # repeat
```

### Functions

```python
def function_name(param1, param2='default'):
    # do something
    return result
```

### List Comprehensions

```python
[x**2 for x in range(10)]              # Squares
[x for x in range(10) if x % 2 == 0]   # Even numbers
```

## Keyboard Shortcuts (Jupyter)

### Command Mode (press Esc)

- `A`: Insert cell above
- `B`: Insert cell below
- `DD`: Delete cell
- `M`: Convert to Markdown
- `Y`: Convert to Code
- `Z`: Undo delete

### Edit Mode (press Enter)

- `Shift + Enter`: Run cell, select below
- `Ctrl + Enter`: Run cell
- `Alt + Enter`: Run cell, insert below
- `Ctrl + /`: Comment/uncomment

## Common pandas Operations

| Operation | Code |
|-----------|------|
| Read CSV | `pd.read_csv('file.csv')` |
| Write CSV | `df.to_csv('file.csv', index=False)` |
| Filter | `df[df['col'] > 5]` |
| Sort | `df.sort_values('col')` |
| Group | `df.groupby('col').mean()` |
| Pivot | `df.pivot_table(values='val', index='row', columns='col')` |
| Merge | `pd.merge(df1, df2, on='id')` |
| Unique | `df['col'].unique()` |
| Value counts | `df['col'].value_counts()` |
| Replace | `df['col'].replace(old, new)` |

## Download Cheat Sheets

- [pandas Cheat Sheet PDF](https://pandas.pydata.org/Pandas_Cheat_Sheet.pdf)
- [NumPy Cheat Sheet](https://numpy.org/doc/stable/user/absolute_beginners.html)
- [Matplotlib Cheat Sheet](https://matplotlib.org/cheatsheets/)
- [Seaborn Tutorial](https://seaborn.pydata.org/tutorial.html)
