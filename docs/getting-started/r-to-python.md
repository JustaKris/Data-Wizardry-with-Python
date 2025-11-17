# R to Python Guide

Welcome R users! This guide will help you leverage your R knowledge to quickly become productive in Python.

## Philosophy Differences

| Aspect | R | Python |
|--------|---|--------|
| **Primary Focus** | Statistical computing | General-purpose programming |
| **Data Structure** | Data frames (built-in) | Data frames (via pandas) |
| **Indexing** | 1-based | 0-based |
| **Assignment** | `<-` or `=` | `=` |
| **Packages** | CRAN, install.packages() | PyPI, pip install |

## Installation & Setup

### R
```r
install.packages("dplyr")
library(dplyr)
```

### Python
```python
# Install (in terminal)
pip install pandas

# Import
import pandas as pd
```

## Reading Data

### R
```r
# CSV
df <- read.csv("data.csv")

# Excel
library(readxl)
df <- read_excel("data.xlsx")

# Built-in data
data(iris)
```

### Python
```python
# CSV
df = pd.read_csv("data.csv")

# Excel
df = pd.read_excel("data.xlsx")

# Built-in data
from sklearn.datasets import load_iris
iris = load_iris(as_frame=True)
```

## Data Inspection

### R
```r
head(df)
tail(df)
str(df)
summary(df)
dim(df)
names(df)
```

### Python
```python
df.head()
df.tail()
df.info()
df.describe()
df.shape
df.columns
```

## Selecting Columns

### R
```r
# Single column
df$column_name
df[, "column_name"]

# Multiple columns
df[, c("col1", "col2")]

# dplyr
df %>% select(col1, col2)
```

### Python
```python
# Single column
df['column_name']
df.column_name  # if no spaces in name

# Multiple columns
df[['col1', 'col2']]

# Method chaining
df.filter(['col1', 'col2'])
```

## Filtering Rows

### R
```r
# Base R
df[df$age > 25, ]

# dplyr
df %>% filter(age > 25)

# Multiple conditions
df %>% filter(age > 25 & dept == "Sales")
```

### Python
```python
# Basic
df[df['age'] > 25]

# Multiple conditions (use &, |, ~)
df[(df['age'] > 25) & (df['dept'] == "Sales")]

# Query method (more readable)
df.query('age > 25 & dept == "Sales"')
```

## Creating New Columns

### R
```r
# Base R
df$new_col <- df$col1 + df$col2

# dplyr
df <- df %>% mutate(new_col = col1 + col2)
```

### Python
```python
# Direct assignment
df['new_col'] = df['col1'] + df['col2']

# Using assign (method chaining)
df = df.assign(new_col = lambda x: x['col1'] + x['col2'])
```

## Grouping and Aggregating

### R
```r
# dplyr
df %>%
  group_by(department) %>%
  summarize(
    avg_salary = mean(salary),
    count = n()
  )
```

### Python
```python
# pandas
df.groupby('department').agg({
    'salary': ['mean', 'count']
})

# Or more explicitly
df.groupby('department')['salary'].agg(['mean', 'count'])
```

## Sorting

### R
```r
# Base R
df[order(df$age), ]

# dplyr
df %>% arrange(age)
df %>% arrange(desc(age))
```

### Python
```python
# pandas
df.sort_values('age')
df.sort_values('age', ascending=False)

# Multiple columns
df.sort_values(['dept', 'age'], ascending=[True, False])
```

## Reshaping Data

### R
```r
# Wide to long
library(tidyr)
df_long <- df %>% pivot_longer(cols = c(Q1, Q2, Q3))

# Long to wide
df_wide <- df %>% pivot_wider(names_from = quarter, values_from = revenue)
```

### Python
```python
# Wide to long
df_long = pd.melt(df, id_vars=['id'], value_vars=['Q1', 'Q2', 'Q3'])

# Long to wide
df_wide = df.pivot(index='id', columns='quarter', values='revenue')
```

## Joining Data

### R
```r
# dplyr
left_join(df1, df2, by = "id")
inner_join(df1, df2, by = "id")
full_join(df1, df2, by = "id")
```

### Python
```python
# pandas
pd.merge(df1, df2, on='id', how='left')
pd.merge(df1, df2, on='id', how='inner')
pd.merge(df1, df2, on='id', how='outer')
```

## Missing Data

### R
```r
# Check for NA
is.na(df$column)

# Remove rows with NA
df %>% drop_na()

# Fill NA
df %>% replace_na(list(column = 0))
```

### Python
```python
# Check for NaN
df['column'].isna()

# Remove rows with NaN
df.dropna()

# Fill NaN
df.fillna(0)
df['column'].fillna(0)
```

## Visualization

### R (ggplot2)
```r
library(ggplot2)

ggplot(df, aes(x = age, y = salary)) +
  geom_point() +
  labs(title = "Salary vs Age")
```

### Python (matplotlib/seaborn)
```python
import matplotlib.pyplot as plt
import seaborn as sns

# matplotlib
plt.scatter(df['age'], df['salary'])
plt.xlabel('Age')
plt.ylabel('Salary')
plt.title('Salary vs Age')
plt.show()

# seaborn (more ggplot2-like)
sns.scatterplot(data=df, x='age', y='salary')
plt.title('Salary vs Age')
plt.show()
```

## Statistical Tests

### R
```r
# t-test
t.test(group1, group2)

# Linear regression
model <- lm(y ~ x1 + x2, data = df)
summary(model)

# ANOVA
aov_result <- aov(value ~ group, data = df)
summary(aov_result)
```

### Python
```python
from scipy import stats
import statsmodels.formula.api as smf

# t-test
stats.ttest_ind(group1, group2)

# Linear regression
model = smf.ols('y ~ x1 + x2', data=df).fit()
print(model.summary())

# ANOVA
model = smf.ols('value ~ C(group)', data=df).fit()
print(stats.f_oneway(group1, group2, group3))
```

## The Pipe Operator

### R (tidyverse)
```r
df %>%
  filter(age > 25) %>%
  group_by(department) %>%
  summarize(avg_salary = mean(salary)) %>%
  arrange(desc(avg_salary))
```

### Python (method chaining)
```python
(df
 .query('age > 25')
 .groupby('department')['salary']
 .mean()
 .sort_values(ascending=False)
)
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

## Quick Reference Card

| Task | R | Python |
|------|---|--------|
| First 6 rows | `head(df)` | `df.head()` |
| Filter | `df %>% filter(x > 5)` | `df[df['x'] > 5]` |
| Select | `df %>% select(a, b)` | `df[['a', 'b']]` |
| Mutate | `df %>% mutate(c = a + b)` | `df['c'] = df['a'] + df['b']` |
| Group & Summarize | `df %>% group_by(g) %>% summarize(m = mean(x))` | `df.groupby('g')['x'].mean()` |
| Sort | `df %>% arrange(x)` | `df.sort_values('x')` |

## Next Steps

- Try the [Python Basics Tutorial](../tutorials/01-python-basics.md)
- Work through `notebooks/01-introduction.ipynb`
- Check out [pandas documentation](https://pandas.pydata.org/docs/)
- Explore the [cheat sheets](../reference/cheatsheets.md)

You'll find that many concepts translate directly. Python just has different syntax for the same ideas you already know!
