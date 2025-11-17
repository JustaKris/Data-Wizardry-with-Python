# Pandas Fundamentals

pandas is the cornerstone library for data analysis in Python. This tutorial covers essential pandas operations.

## What is pandas?

pandas provides high-performance, easy-to-use data structures and data analysis tools. The main data structure is the **DataFrame**, similar to:
- A spreadsheet
- A SQL table
- R's data.frame

## Importing pandas

```python
import pandas as pd
import numpy as np  # Often used together
```

## Creating DataFrames

### From a Dictionary

```python
data = {
    'Name': ['Alice', 'Bob', 'Charlie', 'Diana'],
    'Age': [25, 30, 35, 28],
    'Salary': [50000, 60000, 55000, 52000]
}

df = pd.DataFrame(data)
print(df)
```

### From a List of Lists

```python
data = [
    ['Alice', 25, 50000],
    ['Bob', 30, 60000],
    ['Charlie', 35, 55000]
]

df = pd.DataFrame(data, columns=['Name', 'Age', 'Salary'])
```

### Reading from Files

```python
# CSV
df = pd.read_csv('data.csv')

# Excel
df = pd.read_excel('data.xlsx', sheet_name='Sheet1')

# SPSS
df = pd.read_spss('data.sav')

# With options
df = pd.read_csv('data.csv',
                 sep=';',           # Delimiter
                 decimal=',',       # Decimal character
                 encoding='utf-8',  # File encoding
                 na_values=['NA', 'missing'])  # Missing value markers
```

## Inspecting Data

```python
# First and last rows
df.head()      # First 5 rows
df.head(10)    # First 10 rows
df.tail()      # Last 5 rows

# Shape and size
df.shape       # (rows, columns)
df.size        # Total elements
len(df)        # Number of rows

# Column information
df.columns     # Column names
df.dtypes      # Data types
df.info()      # Comprehensive info

# Statistical summary
df.describe()  # Numeric columns
df.describe(include='all')  # All columns
```

## Selecting Data

### Selecting Columns

```python
# Single column (returns Series)
df['Name']
df.Name  # Only if no spaces in name

# Multiple columns (returns DataFrame)
df[['Name', 'Age']]

# All columns except some
df.drop(['Name'], axis=1)
df.drop(columns=['Name'])
```

### Selecting Rows

```python
# By position
df.iloc[0]      # First row
df.iloc[0:3]    # First 3 rows
df.iloc[-1]     # Last row

# By label/index
df.loc[0]       # Row with index 0
df.loc[0:2]     # Rows 0 to 2 (inclusive!)

# First/last n rows
df.head(10)
df.tail(5)
```

### Selecting Rows and Columns

```python
# Position-based
df.iloc[0:3, 0:2]     # First 3 rows, first 2 columns

# Label-based
df.loc[0:2, ['Name', 'Age']]

# Mixed (avoid if possible)
df.loc[df['Age'] > 25, ['Name', 'Salary']]
```

## Filtering Data

```python
# Single condition
young = df[df['Age'] < 30]

# Multiple conditions (use & and |, with parentheses!)
filtered = df[(df['Age'] > 25) & (df['Salary'] > 50000)]

# OR condition
filtered = df[(df['Age'] < 25) | (df['Salary'] > 60000)]

# NOT condition
filtered = df[~(df['Age'] < 25)]

# Using query() method (more readable)
filtered = df.query('Age > 25 & Salary > 50000')
filtered = df.query('Name == "Alice" | Age > 30')

# Filter by list membership
names_to_keep = ['Alice', 'Bob']
filtered = df[df['Name'].isin(names_to_keep)]
```

## Adding and Modifying Columns

```python
# Add new column
df['Bonus'] = df['Salary'] * 0.1

# Based on conditions
df['Level'] = df['Age'].apply(lambda x: 'Senior' if x > 30 else 'Junior')

# Using np.where (vectorized if-else)
df['Category'] = np.where(df['Salary'] > 55000, 'High', 'Low')

# Multiple conditions with np.select
conditions = [
    df['Salary'] < 52000,
    df['Salary'] < 58000,
    df['Salary'] >= 58000
]
choices = ['Low', 'Medium', 'High']
df['Salary_Band'] = np.select(conditions, choices)

# Modify existing column
df['Salary'] = df['Salary'] * 1.05  # 5% raise
```

## Removing Data

```python
# Drop columns
df = df.drop('Bonus', axis=1)
df = df.drop(columns=['Bonus', 'Level'])

# Drop rows
df = df.drop([0, 1])  # By index
df = df.drop(index=[0, 1])

# Drop duplicates
df = df.drop_duplicates()
df = df.drop_duplicates(subset=['Name'])  # Based on specific columns
```

## Sorting

```python
# Sort by one column
df_sorted = df.sort_values('Age')
df_sorted = df.sort_values('Age', ascending=False)

# Sort by multiple columns
df_sorted = df.sort_values(['Age', 'Salary'], ascending=[True, False])

# Sort by index
df_sorted = df.sort_index()
```

## Grouping and Aggregating

```python
# Group by one column
grouped = df.groupby('Department')['Salary'].mean()

# Multiple aggregations
agg_df = df.groupby('Department')['Salary'].agg(['mean', 'min', 'max', 'count'])

# Different aggregations for different columns
agg_df = df.groupby('Department').agg({
    'Salary': ['mean', 'median'],
    'Age': ['min', 'max']
})

# Custom aggregation
df.groupby('Department')['Salary'].agg(lambda x: x.max() - x.min())

# Group by multiple columns
df.groupby(['Department', 'Level'])['Salary'].mean()
```

## Handling Missing Data

```python
# Detect missing values
df.isnull()          # Boolean DataFrame
df.isnull().sum()    # Count per column
df.isna()            # Same as isnull()

# Drop missing values
df.dropna()          # Drop rows with any NaN
df.dropna(how='all') # Drop only if all values are NaN
df.dropna(subset=['Salary'])  # Drop if NaN in specific column
df.dropna(axis=1)    # Drop columns with NaN

# Fill missing values
df.fillna(0)         # Fill with 0
df.fillna(method='ffill')  # Forward fill
df.fillna(method='bfill')  # Backward fill
df['Salary'].fillna(df['Salary'].mean())  # Fill with mean
```

## Merging and Joining

```python
# Sample data
df1 = pd.DataFrame({'ID': [1, 2, 3], 'Name': ['Alice', 'Bob', 'Charlie']})
df2 = pd.DataFrame({'ID': [1, 2, 4], 'Salary': [50000, 60000, 55000]})

# Inner join (default)
merged = pd.merge(df1, df2, on='ID', how='inner')

# Left join
merged = pd.merge(df1, df2, on='ID', how='left')

# Right join
merged = pd.merge(df1, df2, on='ID', how='right')

# Outer join
merged = pd.merge(df1, df2, on='ID', how='outer')

# Join on different column names
merged = pd.merge(df1, df2, left_on='EmpID', right_on='EmployeeID')

# Concatenate vertically
combined = pd.concat([df1, df2], axis=0)

# Concatenate horizontally
combined = pd.concat([df1, df2], axis=1)
```

## Reshaping Data

### Pivot Tables

```python
# Create pivot table
pivot = df.pivot_table(values='Salary',
                       index='Department',
                       columns='Gender',
                       aggfunc='mean')

# Multiple aggregations
pivot = df.pivot_table(values='Salary',
                       index='Department',
                       aggfunc=['mean', 'count'])
```

### Melting (Wide to Long)

```python
# Wide format
wide_df = pd.DataFrame({
    'ID': [1, 2],
    'Q1': [100, 150],
    'Q2': [110, 160],
    'Q3': [120, 170]
})

# Melt to long format
long_df = pd.melt(wide_df,
                  id_vars=['ID'],
                  var_name='Quarter',
                  value_name='Sales')
```

### Pivoting (Long to Wide)

```python
# Long format
long_df = pd.DataFrame({
    'ID': [1, 1, 2, 2],
    'Quarter': ['Q1', 'Q2', 'Q1', 'Q2'],
    'Sales': [100, 110, 150, 160]
})

# Pivot to wide format
wide_df = long_df.pivot(index='ID',
                        columns='Quarter',
                        values='Sales')
```

## Apply Functions

```python
# Apply to a column
df['Salary_Scaled'] = df['Salary'].apply(lambda x: x / 1000)

# Apply to multiple columns
df[['Age', 'Salary']] = df[['Age', 'Salary']].apply(lambda x: x * 2)

# Apply row-wise
df['Total'] = df.apply(lambda row: row['Salary'] + row['Bonus'], axis=1)

# Using built-in string methods
df['Name_Upper'] = df['Name'].str.upper()
df['Name_Length'] = df['Name'].str.len()
```

## Exporting Data

```python
# To CSV
df.to_csv('output.csv', index=False)

# To Excel
df.to_excel('output.xlsx', sheet_name='Data', index=False)

# Multiple sheets
with pd.ExcelWriter('output.xlsx') as writer:
    df1.to_excel(writer, sheet_name='Sheet1')
    df2.to_excel(writer, sheet_name='Sheet2')

# To SPSS
import pyreadstat
pyreadstat.write_sav(df, 'output.sav')
```

## Common pandas Patterns

### Method Chaining

```python
result = (df
    .query('Age > 25')
    .groupby('Department')['Salary']
    .mean()
    .sort_values(ascending=False)
    .head(5)
)
```

### Resetting Index

```python
# After groupby
df_grouped = df.groupby('Department')['Salary'].mean()
df_grouped = df_grouped.reset_index()  # Convert index to column
```

### Setting Index

```python
df = df.set_index('ID')  # Set ID as index
df = df.reset_index()    # Convert index back to column
```

## Performance Tips

!!! tip "Use vectorized operations"
    ```python
    # Slow (iterating)
    for i in range(len(df)):
        df.loc[i, 'New'] = df.loc[i, 'A'] + df.loc[i, 'B']
    
    # Fast (vectorized)
    df['New'] = df['A'] + df['B']
    ```

!!! tip "Read only needed columns"
    ```python
    df = pd.read_csv('large_file.csv', usecols=['Name', 'Age', 'Salary'])
    ```

!!! tip "Use appropriate data types"
    ```python
    # Convert to categorical for memory savings
    df['Department'] = df['Department'].astype('category')
    ```

## Next Steps

- Continue to [Data Visualization](03-data-visualization.md)
- Practice in `notebooks/02-pandas-fundamentals.ipynb`
- Read the [pandas documentation](https://pandas.pydata.org/docs/)
- Try the [10 Minutes to pandas](https://pandas.pydata.org/docs/user_guide/10min.html) guide

You now have the core pandas skills for data manipulation!
