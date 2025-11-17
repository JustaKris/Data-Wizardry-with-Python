# pandas Overview

**pandas** is the essential Python library for data manipulation and analysis. This guide provides a comprehensive introduction for analysts.

!!! tip "Hands-On Practice"
    For interactive examples using real datasets, see **[notebooks/01_data_loading.ipynb](../../notebooks/01_data_loading.ipynb)** and subsequent notebooks.

## What is pandas?

pandas is built on NumPy and provides:

- **DataFrame**: 2D labeled data structure (like a spreadsheet or SQL table)
- **Series**: 1D labeled array (like a single column)
- **Powerful data manipulation**: filter, group, merge, reshape
- **Time series functionality**: date ranges, resampling, rolling windows
- **I/O tools**: read/write CSV, Excel, SQL, JSON, and more

## Core Concepts

### DataFrame

The primary pandas data structure - a 2D table with labeled rows and columns.

```python
import pandas as pd

# Create from dictionary
data = {
    'name': ['Alice', 'Bob', 'Charlie'],
    'age': [25, 30, 35],
    'city': ['NYC', 'LA', 'Chicago']
}
df = pd.DataFrame(data)
```

### Series

A single column of data with an index.

```python
# Extract a column (returns a Series)
ages = df['age']

# Create a Series directly
s = pd.Series([1, 2, 3, 4], index=['a', 'b', 'c', 'd'])
```

### Index

Row labels that enable fast lookups and alignment.

```python
# Default integer index
df.index  # RangeIndex(start=0, stop=3, step=1)

# Set a column as index
df.set_index('name', inplace=True)

# Reset to default integer index
df.reset_index(inplace=True)
```

## Reading Data

### From CSV

```python
# Basic read
df = pd.read_csv('file.csv')

# With options
df = pd.read_csv(
    'file.csv',
    sep=',',                 # Delimiter
    encoding='utf-8',        # Encoding
    na_values=['NA', ''],    # Treat as missing
    parse_dates=['date'],    # Parse dates
    skiprows=1,              # Skip first row
    nrows=1000               # Read only first 1000 rows
)
```

### From Excel

```python
# Single sheet
df = pd.read_excel('file.xlsx', sheet_name='Sheet1')

# Multiple sheets
sheets = pd.read_excel('file.xlsx', sheet_name=None)  # Returns dict

# Specific range
df = pd.read_excel('file.xlsx', usecols='A:D', nrows=100)
```

### From Other Sources

```python
# JSON
df = pd.read_json('file.json')

# SQL database
import sqlite3
conn = sqlite3.connect('database.db')
df = pd.read_sql('SELECT * FROM table', conn)

# SPSS (requires pyreadstat)
import pyreadstat
df, meta = pyreadstat.read_sav('file.sav')

# Clipboard
df = pd.read_clipboard()  # Paste from Excel!
```

## Inspecting Data

### Quick Overview

```python
# First/last rows
df.head()      # First 5 rows
df.head(10)    # First 10 rows
df.tail()      # Last 5 rows

# Shape and size
df.shape       # (rows, columns)
df.size        # Total elements
len(df)        # Number of rows

# Column info
df.columns     # Column names
df.dtypes      # Data types
df.info()      # Comprehensive summary

# Statistics
df.describe()                    # Numeric columns
df.describe(include='all')       # All columns
df.describe(include=['object'])  # Only text columns
```

### Data Types

```python
# Check types
df.dtypes

# Convert types
df['age'] = df['age'].astype(int)
df['price'] = df['price'].astype(float)
df['date'] = pd.to_datetime(df['date'])
df['category'] = df['category'].astype('category')

# Infer better types
df = df.infer_objects()
```

### Missing Data

```python
# Detect missing
df.isnull()         # Boolean DataFrame
df.isnull().sum()   # Count per column
df.isnull().sum().sum()  # Total missing

# Detect non-missing
df.notnull()

# Check for any missing in each column
df.isnull().any()
```

## Selecting Data

### By Column

```python
# Single column (returns Series)
df['name']
df.name  # Alternative (if name is valid Python identifier)

# Multiple columns (returns DataFrame)
df[['name', 'age']]

# All columns except some
df.drop(['col1', 'col2'], axis=1)
```

### By Row Position (.iloc)

```python
# Single row
df.iloc[0]       # First row
df.iloc[-1]      # Last row

# Multiple rows
df.iloc[0:5]     # First 5 rows
df.iloc[[0, 2, 4]]  # Specific rows

# Rows and columns
df.iloc[0:5, 0:3]    # First 5 rows, first 3 columns
df.iloc[:, [0, 2]]   # All rows, columns 0 and 2
```

### By Label (.loc)

```python
# Single row by index label
df.loc[0]
df.loc['row_name']

# Multiple rows
df.loc[0:5]                # Inclusive end
df.loc[['name1', 'name2']]

# Rows and columns
df.loc[:, 'age']              # All rows, one column
df.loc[:, ['name', 'age']]    # All rows, multiple columns
df.loc[0:5, 'age':'city']     # Row and column slices
```

### Boolean Indexing

```python
# Single condition
df[df['age'] > 30]

# Multiple conditions (use & and |, with parentheses)
df[(df['age'] > 25) & (df['city'] == 'NYC')]
df[(df['age'] < 25) | (df['age'] > 40)]

# Not condition
df[~(df['age'] > 30)]

# isin for multiple values
df[df['city'].isin(['NYC', 'LA'])]

# String contains
df[df['name'].str.contains('Ali')]

# Combine loc with boolean
df.loc[df['age'] > 30, ['name', 'age']]
```

### Query Method

```python
# Alternative to boolean indexing
df.query('age > 30')
df.query('age > 30 and city == "NYC"')
df.query('age > @threshold')  # Use variable with @
```

## Modifying Data

### Adding Columns

```python
# New column from calculation
df['age_squared'] = df['age'] ** 2

# Conditional column
df['category'] = df['age'].apply(lambda x: 'Adult' if x >= 18 else 'Minor')

# Using np.where
import numpy as np
df['status'] = np.where(df['age'] > 30, 'Senior', 'Junior')

# Insert at specific position
df.insert(1, 'new_col', [1, 2, 3])
```

### Removing Columns

```python
# Drop columns
df.drop('column_name', axis=1, inplace=True)
df.drop(['col1', 'col2'], axis=1, inplace=True)

# Alternative
df = df.drop('column_name', axis=1)
```

### Removing Rows

```python
# Drop by index
df.drop(0, inplace=True)
df.drop([0, 1, 2], inplace=True)

# Drop by condition
df = df[df['age'] > 0]

# Drop duplicates
df.drop_duplicates(inplace=True)
df.drop_duplicates(subset=['name'], inplace=True)

# Drop rows with missing values
df.dropna(inplace=True)                      # Any missing
df.dropna(subset=['col1', 'col2'], inplace=True)  # Specific columns
```

### Renaming

```python
# Rename columns
df.rename(columns={'old_name': 'new_name'}, inplace=True)
df.rename(columns={'age': 'years', 'name': 'full_name'}, inplace=True)

# Set column names directly
df.columns = ['new1', 'new2', 'new3']

# Make columns lowercase
df.columns = df.columns.str.lower()
```

## Sorting and Ranking

### Sort by Values

```python
# Sort by one column
df.sort_values('age')
df.sort_values('age', ascending=False)

# Sort by multiple columns
df.sort_values(['city', 'age'])
df.sort_values(['city', 'age'], ascending=[True, False])

# In place
df.sort_values('age', inplace=True)
```

### Sort by Index

```python
df.sort_index()
df.sort_index(ascending=False)
```

### Ranking

```python
df['rank'] = df['age'].rank()
df['rank'] = df['age'].rank(method='dense', ascending=False)
```

## Grouping and Aggregating

### Basic Grouping

```python
# Single aggregation
df.groupby('city')['age'].mean()

# Multiple aggregations on same column
df.groupby('city')['age'].agg(['mean', 'min', 'max'])

# Different aggregations on different columns
df.groupby('city').agg({
    'age': ['mean', 'min', 'max'],
    'salary': 'sum'
})

# Group by multiple columns
df.groupby(['city', 'department'])['salary'].mean()
```

### Common Aggregations

```python
# Available aggregation functions
grouped = df.groupby('city')
grouped.count()     # Count non-null values
grouped.sum()       # Sum
grouped.mean()      # Mean
grouped.median()    # Median
grouped.min()       # Minimum
grouped.max()       # Maximum
grouped.std()       # Standard deviation
grouped.var()       # Variance
grouped.first()     # First value
grouped.last()      # Last value
grouped.size()      # Count including nulls
```

### Transform and Apply

```python
# Transform: same shape as input
df['age_mean_by_city'] = df.groupby('city')['age'].transform('mean')

# Apply: custom function
df.groupby('city')['age'].apply(lambda x: x.max() - x.min())
```

## Merging and Joining

### Merge (SQL-style joins)

```python
# Inner join (default)
pd.merge(df1, df2, on='key')

# Left join
pd.merge(df1, df2, on='key', how='left')

# Right join
pd.merge(df1, df2, on='key', how='right')

# Outer join
pd.merge(df1, df2, on='key', how='outer')

# Different column names
pd.merge(df1, df2, left_on='key1', right_on='key2')

# Multiple keys
pd.merge(df1, df2, on=['key1', 'key2'])
```

### Concatenate

```python
# Vertically (stack rows)
pd.concat([df1, df2])
pd.concat([df1, df2], ignore_index=True)

# Horizontally (add columns)
pd.concat([df1, df2], axis=1)
```

### Join

```python
# Join on index
df1.join(df2)
df1.join(df2, how='left')
```

## Handling Missing Data

### Detect Missing

```python
df.isnull()
df.notnull()
df.isnull().sum()
```

### Remove Missing

```python
# Drop any rows with missing
df.dropna()

# Drop only if all values are missing
df.dropna(how='all')

# Drop based on specific columns
df.dropna(subset=['col1', 'col2'])
```

### Fill Missing

```python
# Fill with specific value
df.fillna(0)
df.fillna({'col1': 0, 'col2': 'Unknown'})

# Forward fill
df.fillna(method='ffill')

# Backward fill
df.fillna(method='bfill')

# Fill with mean
df['age'].fillna(df['age'].mean(), inplace=True)

# Interpolate
df['value'].interpolate(inplace=True)
```

## Writing Data

### To CSV

```python
df.to_csv('output.csv', index=False)
df.to_csv('output.csv', index=False, encoding='utf-8')
df.to_csv('output.csv', columns=['col1', 'col2'])  # Specific columns
```

### To Excel

```python
df.to_excel('output.xlsx', sheet_name='Sheet1', index=False)

# Multiple sheets
with pd.ExcelWriter('output.xlsx') as writer:
    df1.to_excel(writer, sheet_name='Sheet1', index=False)
    df2.to_excel(writer, sheet_name='Sheet2', index=False)
```

### To Other Formats

```python
# JSON
df.to_json('output.json', orient='records')

# SQL
df.to_sql('table_name', conn, if_exists='replace', index=False)

# Clipboard (for pasting into Excel)
df.to_clipboard(index=False)
```

## Best Practices

### Method Chaining

```python
# Instead of multiple statements
df = df[df['age'] > 25]
df = df.sort_values('age')
df = df.reset_index(drop=True)

# Use chaining
df = (df[df['age'] > 25]
      .sort_values('age')
      .reset_index(drop=True))
```

### Copy vs View

```python
# Create a copy to avoid SettingWithCopyWarning
df_subset = df[df['age'] > 25].copy()

# Now safe to modify
df_subset['new_col'] = 1
```

### Performance Tips

1. **Use vectorized operations** instead of loops
2. **Use categorical dtype** for low-cardinality string columns
3. **Read only needed columns**: `usecols` parameter
4. **Use chunks** for large files: `chunksize` parameter
5. **Specify dtypes** when reading to save memory

```python
# Good: vectorized
df['total'] = df['price'] * df['quantity']

# Avoid: loops
for i in range(len(df)):
    df.loc[i, 'total'] = df.loc[i, 'price'] * df.loc[i, 'quantity']
```

## Common Patterns

### Value Counts

```python
# Frequency count
df['city'].value_counts()
df['city'].value_counts(normalize=True)  # Proportions
```

### Pivot Tables

```python
# Spreadsheet-style pivot
df.pivot_table(
    values='salary',
    index='department',
    columns='city',
    aggfunc='mean'
)
```

### Reshaping

```python
# Wide to long
pd.melt(df, id_vars=['id'], value_vars=['Q1', 'Q2', 'Q3'])

# Long to wide
df.pivot(index='id', columns='quarter', values='sales')
```

## Next Steps

- **Practice**: Try the notebooks in `notebooks/`
- **Cheat sheet**: See the [pandas Cheat Sheet](cheat_sheet.md)
- **Official docs**: [pandas.pydata.org](https://pandas.pydata.org/)
- **10 Minutes to pandas**: [Quick tutorial](https://pandas.pydata.org/docs/user_guide/10min.html)
