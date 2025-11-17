# R to Python Guide

Welcome R users! This guide will help you leverage your R knowledge to quickly become productive in Python.

## Core dplyr to pandas Quick Reference

The table below shows the most common R dplyr operations and their pandas equivalents. These are the operations you'll use daily.

### Select Columns

| Operation | R (dplyr) | Python (pandas) |
|-----------|-----------|----------------|
| Select specific columns | `df %>% select(name, age)` | `df[['name', 'age']]` |
| Select by condition | `df %>% select(starts_with("sal"))` | `df.filter(like='sal')` |
| Drop columns | `df %>% select(-age)` | `df.drop(columns=['age'])` |

**Pandas Example:**
```python
import pandas as pd

# Sample data
df = pd.DataFrame({
    'name': ['Alice', 'Bob', 'Charlie'],
    'age': [25, 30, 35],
    'salary': [50000, 60000, 55000],
    'dept': ['Sales', 'IT', 'Sales']
})

# Select specific columns
result = df[['name', 'age']]
```

### Filter Rows

| Operation | R (dplyr) | Python (pandas) |
|-----------|-----------|----------------|
| Simple filter | `df %>% filter(age > 25)` | `df[df['age'] > 25]` |
| Multiple conditions (AND) | `df %>% filter(age > 25 & dept == "Sales")` | `df[(df['age'] > 25) & (df['dept'] == 'Sales')]` |
| Multiple conditions (OR) | `df %>% filter(age > 25 \| dept == "Sales")` | `df[(df['age'] > 25) \| (df['dept'] == 'Sales')]` |
| Using query (cleaner) | N/A | `df.query('age > 25 & dept == "Sales"')` |

**Pandas Example:**
```python
# Filter rows where age > 25
result = df[df['age'] > 25]

# Multiple conditions - need parentheses and & instead of 'and'
result = df[(df['age'] > 25) & (df['dept'] == 'Sales')]

# Using query method (more readable)
result = df.query('age > 25 & dept == "Sales"')
```

### Create/Modify Columns (Mutate)

| Operation | R (dplyr) | Python (pandas) |
|-----------|-----------|----------------|
| Create new column | `df %>% mutate(bonus = salary * 0.1)` | `df['bonus'] = df['salary'] * 0.1` |
| Multiple columns | `df %>% mutate(bonus = salary * 0.1, total = salary + bonus)` | `df.assign(bonus=df['salary'] * 0.1).assign(total=lambda x: x['salary'] + x['bonus'])` |
| Conditional column | `df %>% mutate(senior = if_else(age > 30, "Yes", "No"))` | `df['senior'] = df['age'].apply(lambda x: 'Yes' if x > 30 else 'No')` or `np.where(df['age'] > 30, 'Yes', 'No')` |

**Pandas Example:**
```python
import numpy as np

# Create new column
df['bonus'] = df['salary'] * 0.1

# Create multiple columns
df['bonus'] = df['salary'] * 0.1
df['total_comp'] = df['salary'] + df['bonus']

# Method chaining with assign
df = df.assign(
    bonus=lambda x: x['salary'] * 0.1,
    total_comp=lambda x: x['salary'] + x['bonus']
)

# Conditional column
df['senior'] = np.where(df['age'] > 30, 'Yes', 'No')
# Or using apply
df['senior'] = df['age'].apply(lambda x: 'Yes' if x > 30 else 'No')
```

### Group By and Summarise

| Operation | R (dplyr) | Python (pandas) |
|-----------|-----------|----------------|
| Single aggregation | `df %>% group_by(dept) %>% summarise(avg_sal = mean(salary))` | `df.groupby('dept')['salary'].mean()` |
| Multiple aggregations | `df %>% group_by(dept) %>% summarise(avg_sal = mean(salary), count = n())` | `df.groupby('dept')['salary'].agg(['mean', 'count'])` |
| Multiple columns | `df %>% group_by(dept) %>% summarise(avg_sal = mean(salary), avg_age = mean(age))` | `df.groupby('dept').agg({'salary': 'mean', 'age': 'mean'})` |
| Multiple groups | `df %>% group_by(dept, senior) %>% summarise(avg_sal = mean(salary))` | `df.groupby(['dept', 'senior'])['salary'].mean()` |

**Pandas Example:**
```python
# Single aggregation
result = df.groupby('dept')['salary'].mean()

# Multiple aggregations on same column
result = df.groupby('dept')['salary'].agg(['mean', 'count', 'min', 'max'])

# Multiple aggregations on different columns
result = df.groupby('dept').agg({
    'salary': ['mean', 'sum'],
    'age': ['mean', 'min', 'max']
})

# Multiple grouping variables
result = df.groupby(['dept', 'senior'])['salary'].mean()

# With custom names (pandas 0.25+)
result = df.groupby('dept').agg(
    avg_salary=('salary', 'mean'),
    count=('salary', 'size'),
    max_age=('age', 'max')
)
```

### Join/Merge DataFrames

| Operation | R (dplyr) | Python (pandas) |
|-----------|-----------|----------------|
| Left join | `left_join(df1, df2, by = "id")` | `pd.merge(df1, df2, on='id', how='left')` |
| Inner join | `inner_join(df1, df2, by = "id")` | `pd.merge(df1, df2, on='id', how='inner')` |
| Full outer join | `full_join(df1, df2, by = "id")` | `pd.merge(df1, df2, on='id', how='outer')` |
| Join on different columns | `left_join(df1, df2, by = c("id1" = "id2"))` | `pd.merge(df1, df2, left_on='id1', right_on='id2', how='left')` |

**Pandas Example:**
```python
# Sample data for joins
df1 = pd.DataFrame({
    'id': [1, 2, 3],
    'name': ['Alice', 'Bob', 'Charlie']
})

df2 = pd.DataFrame({
    'id': [1, 2, 4],
    'salary': [50000, 60000, 55000]
})

# Left join - keep all rows from df1
result = pd.merge(df1, df2, on='id', how='left')

# Inner join - only matching rows
result = pd.merge(df1, df2, on='id', how='inner')

# Outer join - all rows from both
result = pd.merge(df1, df2, on='id', how='outer')

# Join on different column names
result = pd.merge(df1, df2, left_on='id', right_on='employee_id', how='left')
```

---

## Philosophy Differences

| Aspect | R | Python |
|--------|---|--------|
| **Primary Focus** | Statistical computing | General-purpose programming |
| **Data Structure** | Data frames (built-in) | Data frames (via pandas) |
| **Indexing** | 1-based | 0-based |
| **Assignment** | `<-` or `=` | `=` |
| **Packages** | CRAN, install.packages() | PyPI, pip install |


## Additional Operations

### Installation & Setup

***R***

```r
install.packages("dplyr")
library(dplyr)
```

***Python***

```python
# Install (in terminal)
pip install pandas

# Import
import pandas as pd
```

### Reading Data

***R***

```r
# CSV
df <- read.csv("data.csv")

# Excel
library(readxl)
df <- read_excel("data.xlsx")
```

***Python***

```python
# CSV
df = pd.read_csv("data.csv")

# Excel
df = pd.read_excel("data.xlsx")

# Using local data files
df = pd.read_csv("data/socio_demos.csv")
```

### Data Inspection

| R | Python |
|---|--------|
| `head(df)` | `df.head()` |
| `tail(df)` | `df.tail()` |
| `str(df)` | `df.info()` |
| `summary(df)` | `df.describe()` |
| `dim(df)` | `df.shape` |
| `names(df)` | `df.columns` |

### Sorting

***R***

```r
# dplyr
df %>% arrange(age)
df %>% arrange(desc(age))
```

***Python***

```python
# pandas
df.sort_values('age')
df.sort_values('age', ascending=False)

# Multiple columns
df.sort_values(['dept', 'age'], ascending=[True, False])
```

### Reshaping Data

***R***

```r
# Wide to long
library(tidyr)
df_long <- df %>% pivot_longer(cols = c(Q1, Q2, Q3))

# Long to wide
df_wide <- df %>% pivot_wider(names_from = quarter, values_from = revenue)
```

***Python***

```python
# Wide to long
df_long = pd.melt(df, id_vars=['id'], value_vars=['Q1', 'Q2', 'Q3'])

# Long to wide
df_wide = df.pivot(index='id', columns='quarter', values='revenue')
```


### Missing Data

***R***

```r
# Check for NA
is.na(df$column)

# Remove rows with NA
df %>% drop_na()

# Fill NA
df %>% replace_na(list(column = 0))
```

***Python***

```python
# Check for NaN
df['column'].isna()

# Remove rows with NaN
df.dropna()

# Fill NaN
df.fillna(0)
df['column'].fillna(0)
```

### The Pipe Operator / Method Chaining

***R*** (tidyverse)

```r
df %>%
  filter(age > 25) %>%
  group_by(department) %>%
  summarize(avg_salary = mean(salary)) %>%
  arrange(desc(avg_salary))
```

***Python*** (method chaining)

```python
(df
 .query('age > 25')
 .groupby('department')['salary']
 .mean()
 .sort_values(ascending=False)
)
```

## Visualization

***R*** (ggplot2)

```r
library(ggplot2)

ggplot(df, aes(x = age, y = salary)) +
  geom_point() +
  labs(title = "Salary vs Age")
```

***Python*** (seaborn - most ggplot2-like)

```python
import matplotlib.pyplot as plt
import seaborn as sns

sns.scatterplot(data=df, x='age', y='salary')
plt.title('Salary vs Age')
plt.show()
```

## Statistical Tests

***R***

```r
# t-test
t.test(group1, group2)

# Linear regression
model <- lm(y ~ x1 + x2, data = df)
summary(model)
```

***Python***

```python
from scipy import stats
import statsmodels.formula.api as smf

# t-test
stats.ttest_ind(group1, group2)

# Linear regression
model = smf.ols('y ~ x1 + x2', data=df).fit()
print(model.summary())
```

## Pro Tips for R Users

!!! tip "Embrace 0-based indexing"
    Remember: Python uses 0-based indexing. The first element is at position 0.

!!! tip "Use parentheses for conditions"
    When filtering with multiple conditions, wrap each in parentheses: `(df['a'] > 5) & (df['b'] < 10)`

!!! tip "Think in methods"
    Python/pandas uses methods: `df.method()` instead of R's `function(df)`

!!! tip "Try method chaining"
    Like R's pipe (`%>%`), Python allows chaining: `df.filter().groupby().mean()`

!!! warning "Watch out for copies vs views"
    In pandas, some operations return views, others return copies. Use `.copy()` when unsure.

## Next Steps

- Try the [Python Basics Tutorial](../tutorials/01-python-basics.md)
- Work through the notebooks in the `notebooks/` directory
- Experiment with the data files in `data/` directory
- Check out [pandas documentation](https://pandas.pydata.org/docs/)
- Explore the [cheat sheets](../reference/cheatsheets.md)

You'll find that many concepts translate directly. Python just has different syntax for the same ideas you already know!
