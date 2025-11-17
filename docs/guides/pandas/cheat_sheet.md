# pandas Cheat Sheet

Quick reference for common pandas operations.

!!! info "See Also"
    For complete examples with real data, check out the **[notebooks](../../notebooks/)** folder, starting with **[01_data_loading.ipynb](../../notebooks/01_data_loading.ipynb)**.

## Import

```python
import pandas as pd
import numpy as np
```

## Reading Data

```python
pd.read_csv('file.csv')
pd.read_csv('file.csv', sep=';', encoding='utf-8')
pd.read_excel('file.xlsx', sheet_name='Sheet1')
pd.read_json('file.json')
pd.read_sql('SELECT * FROM table', conn)
pd.read_clipboard()  # From clipboard
```

## Viewing Data

```python
df.head()           # First 5 rows
df.head(10)         # First 10 rows
df.tail()           # Last 5 rows
df.shape            # (rows, columns)
df.columns          # Column names
df.dtypes           # Data types
df.info()           # Overview
df.describe()       # Statistics (numeric)
df.describe(include='all')  # All columns
```

## Selecting Data

### Columns

```python
df['column']                    # Single column (Series)
df[['col1', 'col2']]           # Multiple columns (DataFrame)
df.drop('col', axis=1)          # Drop column
```

### Rows

```python
df.iloc[0]                      # First row by position
df.iloc[0:5]                    # First 5 rows
df.iloc[[0, 2, 4]]             # Specific rows by position
df.loc[0]                       # Row by index label
df.loc[0:5]                     # Slice by label (inclusive)
```

### Conditional

```python
df[df['age'] > 25]                          # Filter rows
df[(df['age'] > 25) & (df['city'] == 'NYC')]  # Multiple conditions
df[df['city'].isin(['NYC', 'LA'])]          # Multiple values
df.query('age > 25 and city == "NYC"')      # Query string
df.loc[df['age'] > 25, ['name', 'age']]     # Specific columns
```

## Creating Columns

```python
df['new'] = df['a'] + df['b']               # From calculation
df['category'] = df['age'].apply(lambda x: 'Adult' if x >= 18 else 'Minor')
df['status'] = np.where(df['age'] > 30, 'Senior', 'Junior')
```

## Removing Data

```python
df.drop('col', axis=1, inplace=True)        # Drop column
df.drop([0, 1], inplace=True)               # Drop rows by index
df.dropna()                                  # Drop rows with missing
df.dropna(subset=['col'])                   # Drop if specific column missing
df.drop_duplicates()                        # Drop duplicate rows
df.drop_duplicates(subset=['col'])          # Based on specific column
```

## Sorting

```python
df.sort_values('col')                       # Sort by column
df.sort_values('col', ascending=False)      # Descending
df.sort_values(['col1', 'col2'])           # Multiple columns
df.sort_index()                             # Sort by index
```

## Grouping and Aggregating

```python
df.groupby('col').mean()                    # Group and aggregate
df.groupby('col')['value'].mean()          # Specific column
df.groupby('col').agg(['mean', 'sum'])     # Multiple aggregations
df.groupby('col').agg({                     # Different aggs per column
    'val1': 'mean',
    'val2': ['sum', 'count']
})
df.groupby(['col1', 'col2']).mean()        # Multiple grouping columns
```

## Merging and Joining

```python
pd.merge(df1, df2, on='key')                       # Inner join
pd.merge(df1, df2, on='key', how='left')          # Left join
pd.merge(df1, df2, on='key', how='outer')         # Outer join
pd.merge(df1, df2, left_on='k1', right_on='k2')   # Different key names
pd.concat([df1, df2])                              # Append rows
pd.concat([df1, df2], axis=1)                      # Append columns
```

## Missing Data

```python
df.isnull()                                 # Check for missing
df.isnull().sum()                          # Count missing per column
df.dropna()                                 # Drop rows with any missing
df.dropna(how='all')                       # Drop only if all missing
df.fillna(0)                               # Fill with value
df.fillna({'col1': 0, 'col2': 'Unknown'})  # Different values per column
df['col'].fillna(df['col'].mean())         # Fill with mean
```

## Data Types

```python
df.dtypes                                   # Check types
df['col'].astype(int)                      # Convert type
df['col'].astype('category')               # To categorical
pd.to_datetime(df['col'])                  # To datetime
pd.to_numeric(df['col'], errors='coerce')  # To numeric (invalid → NaN)
```

## String Operations

```python
df['col'].str.lower()                      # Lowercase
df['col'].str.upper()                      # Uppercase
df['col'].str.strip()                      # Remove whitespace
df['col'].str.replace('old', 'new')        # Replace
df['col'].str.contains('pattern')          # Contains
df['col'].str.split(',')                   # Split
df['col'].str[0:5]                         # Slice
```

## Value Counts and Unique

```python
df['col'].unique()                         # Unique values
df['col'].nunique()                        # Count unique
df['col'].value_counts()                   # Frequency count
df['col'].value_counts(normalize=True)     # Proportions
```

## Reshaping

```python
# Pivot table
df.pivot_table(
    values='sales',
    index='month',
    columns='region',
    aggfunc='sum'
)

# Wide to long
pd.melt(df, id_vars=['id'], value_vars=['Q1', 'Q2'])

# Long to wide
df.pivot(index='id', columns='quarter', values='sales')
```

## Apply and Map

```python
df['col'].apply(lambda x: x * 2)           # Apply function to Series
df.apply(lambda row: row['a'] + row['b'], axis=1)  # Apply to rows
df['col'].map({'old': 'new'})              # Map values
df.applymap(lambda x: x * 2)               # Apply to all elements (deprecated, use df.map())
```

## Datetime Operations

```python
pd.to_datetime(df['col'])                  # Convert to datetime
df['year'] = df['date'].dt.year            # Extract year
df['month'] = df['date'].dt.month          # Extract month
df['day'] = df['date'].dt.day              # Extract day
df['dayofweek'] = df['date'].dt.dayofweek  # Day of week (0=Monday)
```

## Writing Data

```python
df.to_csv('file.csv', index=False)
df.to_csv('file.csv', index=False, encoding='utf-8')
df.to_excel('file.xlsx', sheet_name='Sheet1', index=False)
df.to_json('file.json', orient='records')
df.to_sql('table', conn, if_exists='replace', index=False)
df.to_clipboard(index=False)               # Copy to clipboard
```

## Common Patterns

### Rename Columns

```python
df.rename(columns={'old': 'new'}, inplace=True)
df.columns = ['new1', 'new2', 'new3']
df.columns = df.columns.str.lower()        # Make lowercase
```

### Replace Values

```python
df['col'].replace('old', 'new')
df['col'].replace(['old1', 'old2'], ['new1', 'new2'])
df['col'].replace({'old1': 'new1', 'old2': 'new2'})
```

### Filter and Select

```python
# Select specific columns for specific rows
df.loc[df['age'] > 25, ['name', 'age']]

# Top N rows
df.nlargest(10, 'salary')
df.nsmallest(10, 'age')

# Sample random rows
df.sample(10)
df.sample(frac=0.1)  # 10% of rows
```

### Copy to Avoid Warnings

```python
df_subset = df[df['age'] > 25].copy()
```

### Method Chaining

```python
result = (df
    .query('age > 25')
    .groupby('city')['salary']
    .mean()
    .reset_index()
    .sort_values('salary', ascending=False)
)
```

## Comparison with Other Tools

### R (dplyr)

| R (dplyr) | pandas |
|-----------|--------|
| `filter()` | `df[df['col'] > 5]` or `df.query()` |
| `select()` | `df[['col1', 'col2']]` |
| `mutate()` | `df['new'] = ...` |
| `arrange()` | `df.sort_values()` |
| `group_by() %>% summarize()` | `df.groupby().agg()` |
| `left_join()` | `pd.merge(..., how='left')` |

### SQL

| SQL | pandas |
|-----|--------|
| `SELECT col1, col2 FROM table` | `df[['col1', 'col2']]` |
| `WHERE age > 25` | `df[df['age'] > 25]` |
| `ORDER BY col` | `df.sort_values('col')` |
| `GROUP BY col` | `df.groupby('col')` |
| `COUNT(*)` | `df.groupby('col').size()` |
| `LEFT JOIN` | `pd.merge(..., how='left')` |

## Performance Tips

1. Use vectorized operations instead of loops
2. Use `.loc` or `.iloc` for selection (not chained indexing)
3. Specify `dtype` when reading data to save memory
4. Use `category` dtype for low-cardinality strings
5. Use `query()` for complex filters (can be faster)
6. Read large files in chunks with `chunksize`

```python
# Good (vectorized)
df['total'] = df['price'] * df['quantity']

# Bad (loop)
for i in range(len(df)):
    df.loc[i, 'total'] = df.loc[i, 'price'] * df.loc[i, 'quantity']
```

## Common Errors and Solutions

### SettingWithCopyWarning

```python
# Problem
df_subset = df[df['age'] > 25]
df_subset['new_col'] = 1  # Warning!

# Solution
df_subset = df[df['age'] > 25].copy()
df_subset['new_col'] = 1  # OK
```

### KeyError: 'column_name'

```python
# Check if column exists
'column_name' in df.columns

# List all columns
df.columns.tolist()
```

### ValueError: Length mismatch

```python
# When assigning a new column, length must match
len(df) == len(new_values)  # Must be True
```

## Resources

- **Official docs**: [pandas.pydata.org/docs](https://pandas.pydata.org/docs/)
- **10 Minutes to pandas**: [Quick tutorial](https://pandas.pydata.org/docs/user_guide/10min.html)
- **Cheat Sheet PDF**: [Download](https://pandas.pydata.org/Pandas_Cheat_Sheet.pdf)
- **User Guide**: [Comprehensive guide](https://pandas.pydata.org/docs/user_guide/index.html)
