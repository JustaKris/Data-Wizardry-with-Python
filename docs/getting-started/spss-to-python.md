# SPSS to Python Guide

Welcome SPSS users! This guide will help you translate your SPSS knowledge into Python for data analysis.

## Why Transition from SPSS to Python?

- **Cost**: Python is free and open-source
- **Flexibility**: Full programming language, not just statistical procedures
- **Integration**: Easily connect to databases, APIs, and web services
- **Reproducibility**: Code-based analysis is easier to document and share
- **Community**: Large, active community with extensive packages

## Reading SPSS Files in Python

Python can read SPSS `.sav` files directly!

### Using pyreadstat

```python
import pandas as pd
import pyreadstat

# Read SPSS file
df, meta = pyreadstat.read_sav('data.sav')

# View data
print(df.head())

# View metadata (variable labels, value labels, etc.)
print(meta.column_names_to_labels)
print(meta.variable_value_labels)
```

### Using pandas (newer SPSS files)

```python
import pandas as pd

# Read SPSS file
df = pd.read_spss('data.sav')
```

## Common SPSS Procedures in Python

### FREQUENCIES

**SPSS:**

```spss
FREQUENCIES VARIABLES=gender department
  /ORDER=ANALYSIS.
```

**Python:**

```python
# Single variable
print(df['gender'].value_counts())

# Multiple variables
for col in ['gender', 'department']:
    print(f"\nFrequencies for {col}:")
    print(df[col].value_counts())

# With percentages
print(df['gender'].value_counts(normalize=True) * 100)
```

### DESCRIPTIVES

**SPSS:**

```spss
DESCRIPTIVES VARIABLES=age salary
  /STATISTICS=MEAN STDDEV MIN MAX.
```

**Python:**

```python
# Basic descriptives
print(df[['age', 'salary']].describe())

# Specific statistics
print(df[['age', 'salary']].agg(['mean', 'std', 'min', 'max']))
```

### CROSSTABS

**SPSS:**

```spss
CROSSTABS
  /TABLES=department BY gender
  /STATISTICS=CHISQ.
```

**Python:**

```python
# Create crosstab
crosstab = pd.crosstab(df['department'], df['gender'])
print(crosstab)

# Chi-square test
from scipy.stats import chi2_contingency

chi2, p_value, dof, expected = chi2_contingency(crosstab)
print(f"Chi-square: {chi2}")
print(f"p-value: {p_value}")
```

### T-TEST

**SPSS:**

```spss
T-TEST GROUPS=gender(0 1)
  /VARIABLES=salary.
```

**Python:**

```python
from scipy import stats

# Split groups
group1 = df[df['gender'] == 0]['salary']
group2 = df[df['gender'] == 1]['salary']

# Independent t-test
t_stat, p_value = stats.ttest_ind(group1, group2)
print(f"t-statistic: {t_stat}")
print(f"p-value: {p_value}")
```

### ONEWAY ANOVA

**SPSS:**

```spss
ONEWAY salary BY department
  /STATISTICS=DESCRIPTIVES
  /POSTHOC=TUKEY.
```

**Python:**

```python
from scipy import stats
import statsmodels.api as sm
from statsmodels.formula.api import ols
from statsmodels.stats.multicomp import pairwise_tukeyhsd

# One-way ANOVA
groups = [group['salary'].values for name, group in df.groupby('department')]
f_stat, p_value = stats.f_oneway(*groups)
print(f"F-statistic: {f_stat}")
print(f"p-value: {p_value}")

# With more detail using statsmodels
model = ols('salary ~ C(department)', data=df).fit()
anova_table = sm.stats.anova_lm(model, typ=2)
print(anova_table)

# Post-hoc Tukey test
tukey = pairwise_tukeyhsd(endog=df['salary'], groups=df['department'])
print(tukey)
```

### REGRESSION

**SPSS:**

```spss
REGRESSION
  /DEPENDENT salary
  /METHOD=ENTER age experience education.
```

**Python:**

```python
import statsmodels.formula.api as smf

# Linear regression
model = smf.ols('salary ~ age + experience + education', data=df).fit()
print(model.summary())

# Get coefficients
print(model.params)

# Get R-squared
print(f"R-squared: {model.rsquared}")
```

### CORRELATION

**SPSS:**

```spss
CORRELATIONS
  /VARIABLES=age salary experience
  /PRINT=TWOTAIL NOSIG.
```

**Python:**

```python
# Pearson correlation matrix
corr_matrix = df[['age', 'salary', 'experience']].corr()
print(corr_matrix)

# With p-values
from scipy.stats import pearsonr

r, p = pearsonr(df['age'], df['salary'])
print(f"Correlation: {r}")
print(f"p-value: {p}")
```

## Data Manipulation

### SELECT IF

**SPSS:**

```spss
SELECT IF (age >= 25 AND department = 'Sales').
```

**Python:**

```python
# Filter data
filtered_df = df[(df['age'] >= 25) & (df['department'] == 'Sales')]
```

### COMPUTE

**SPSS:**

```spss
COMPUTE total_comp = salary + bonus.
```

**Python:**

```python
# Create new variable
df['total_comp'] = df['salary'] + df['bonus']
```

### RECODE

**SPSS:**

```spss
RECODE age (18 thru 30=1) (31 thru 50=2) (51 thru 99=3) INTO age_group.
```

**Python:**

```python
# Using cut
df['age_group'] = pd.cut(df['age'], 
                          bins=[0, 30, 50, 100], 
                          labels=[1, 2, 3])

# Or using conditions
import numpy as np
conditions = [
    (df['age'] <= 30),
    (df['age'] <= 50),
    (df['age'] > 50)
]
df['age_group'] = np.select(conditions, [1, 2, 3])
```

### SORT CASES

**SPSS:**

```spss
SORT CASES BY department age (D).
```

**Python:**

```python
# Sort data
df = df.sort_values(['department', 'age'], ascending=[True, False])
```

### AGGREGATE

**SPSS:**

```spss
AGGREGATE
  /OUTFILE=* MODE=ADDVARIABLES
  /BREAK=department
  /mean_salary=MEAN(salary).
```

**Python:**

```python
# Group statistics
df['mean_salary'] = df.groupby('department')['salary'].transform('mean')
```

## Creating Tables

### Custom Tables

**SPSS:**

```spss
CTABLES
  /TABLE department BY salary [MEAN]
```

**Python:**

```python
# Pivot table
table = df.pivot_table(values='salary', 
                       index='department', 
                       aggfunc='mean')
print(table)

# More complex
table = df.pivot_table(values='salary',
                       index='department',
                       columns='gender',
                       aggfunc=['mean', 'count'])
print(table)
```

## Charts and Graphs

### Bar Chart

**SPSS:**

```spss
GRAPH
  /BAR=COUNT BY department.
```

**Python:**

```python
import matplotlib.pyplot as plt

# Bar chart
df['department'].value_counts().plot(kind='bar')
plt.title('Count by Department')
plt.xlabel('Department')
plt.ylabel('Count')
plt.show()
```

### Histogram

**SPSS:**

```spss
GRAPH
  /HISTOGRAM=salary.
```

**Python:**

```python
# Histogram
df['salary'].hist(bins=20)
plt.title('Salary Distribution')
plt.xlabel('Salary')
plt.ylabel('Frequency')
plt.show()
```

### Scatterplot

**SPSS:**

```spss
GRAPH
  /SCATTERPLOT=age WITH salary.
```

**Python:**

```python
# Scatter plot
plt.scatter(df['age'], df['salary'])
plt.title('Salary vs Age')
plt.xlabel('Age')
plt.ylabel('Salary')
plt.show()

# Or with seaborn (more features)
import seaborn as sns
sns.scatterplot(data=df, x='age', y='salary', hue='department')
plt.show()
```

## Missing Values

### SPSS

```spss
RECODE age (SYSMIS=99).
```

### Python

```python
# Check for missing
print(df.isnull().sum())

# Fill missing
df['age'].fillna(99, inplace=True)

# Drop rows with missing
df_clean = df.dropna()

# Drop columns with missing
df_clean = df.dropna(axis=1)
```

## Saving Output

### Export to SPSS

**Python:**

```python
# Save as SPSS file
pyreadstat.write_sav(df, 'output.sav')
```

### Export to Excel

**Python:**

```python
# Save to Excel
df.to_excel('output.xlsx', index=False)

# Multiple sheets
with pd.ExcelWriter('output.xlsx') as writer:
    df.to_excel(writer, sheet_name='Data', index=False)
    summary.to_excel(writer, sheet_name='Summary', index=False)
```

### Export to CSV

**Python:**

```python
# Save to CSV
df.to_csv('output.csv', index=False)
```

## Working with Variable Labels

### Preserve SPSS metadata

```python
import pyreadstat

# Read with metadata
df, meta = pyreadstat.read_sav('data.sav')

# Access variable labels
labels = meta.column_names_to_labels
print(labels)

# Access value labels
value_labels = meta.variable_value_labels
print(value_labels['gender'])

# Write back with labels
pyreadstat.write_sav(df, 'output.sav',
                     column_labels=labels,
                     variable_value_labels=value_labels)
```

## Quick Reference

| SPSS Command | Python Equivalent |
|--------------|-------------------|
| `FREQUENCIES` | `df['col'].value_counts()` |
| `DESCRIPTIVES` | `df.describe()` |
| `CROSSTABS` | `pd.crosstab()` |
| `T-TEST` | `scipy.stats.ttest_ind()` |
| `REGRESSION` | `statsmodels.ols().fit()` |
| `CORRELATIONS` | `df.corr()` |
| `SELECT IF` | `df[df['col'] > value]` |
| `COMPUTE` | `df['new'] = df['a'] + df['b']` |
| `SORT CASES` | `df.sort_values()` |
| `AGGREGATE` | `df.groupby().agg()` |

## Pro Tips for SPSS Users

!!! tip "Think in Data Frames"
    In Python, everything is a DataFrame object. Operations are methods: `df.method()`

!!! tip "Use Jupyter Notebooks"
    Jupyter notebooks are like SPSS syntax files but interactive and visual

!!! tip "Leverage Libraries"
    - **pandas**: Data manipulation (like SPSS data editor)
    - **scipy**: Statistical tests
    - **statsmodels**: Regression and advanced stats
    - **matplotlib/seaborn**: Graphics

!!! warning "0-based Indexing"
    Python uses 0-based indexing. The first row/column is at position 0.

!!! success "Automation"
    Python excels at automation. One script can process multiple files, generate reports, etc.

## Next Steps

- Work through the [Quick Start Guide](quickstart.md)
- Try `notebooks/01-introduction.ipynb`
- Explore the [Statistical Analysis Tutorial](../tutorials/04-statistical-analysis.md)
- Check the [Cheat Sheets](../reference/cheatsheets.md)

The transition from SPSS to Python opens up powerful new possibilities for your analysis!
