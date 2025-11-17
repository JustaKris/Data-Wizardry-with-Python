# SPSS to Python Guide

Welcome SPSS users! This guide will help you translate your SPSS knowledge into Python for data analysis.

## Why Transition from SPSS to Python?

- **Cost**: Python is free and open-source
- **Flexibility**: Full programming language, not just statistical procedures
- **Integration**: Easily connect to databases, APIs, and web services
- **Reproducibility**: Code-based analysis is easier to document and share
- **Community**: Large, active community with extensive packages

## Core SPSS to Python Quick Reference

### Data Management

| Operation | SPSS | Python (pandas) |
|-----------|------|-----------------|
| Read CSV | `GET DATA /TYPE=TXT /FILE="data.csv"` | `df = pd.read_csv("data.csv")` |
| Read SPSS file | Open in SPSS | `df = pd.read_spss("data.sav")` or `df, meta = pyreadstat.read_sav("data.sav")` |
| View data | Data View | `df.head()` or open in VS Code |
| Select cases | `SELECT IF (age > 25)` | `df = df[df['age'] > 25]` |
| Compute variable | `COMPUTE total = var1 + var2` | `df['total'] = df['var1'] + df['var2']` |
| Recode variable | `RECODE age (18 thru 30=1) (31 thru 50=2)` | `df['age_group'] = pd.cut(df['age'], bins=[18, 30, 50, 100], labels=[1, 2, 3])` |
| Sort cases | `SORT CASES BY age (D)` | `df = df.sort_values('age', ascending=False)` |

**Pandas Example:**

```python
import pandas as pd

# Read data (using provided sample data)
df = pd.read_csv("data/socio_demos.csv")

# View first few rows
print(df.head())

# Select cases (filter)
adults = df[df['age'] > 18]

# Compute new variable
df['age_squared'] = df['age'] ** 2

# Sort by age descending
df = df.sort_values('age', ascending=False)
```

### Descriptive Statistics

| Procedure | SPSS | Python (pandas) |
|-----------|------|-----------------|
| Frequencies | `FREQUENCIES VARIABLES=gender` | `df['gender'].value_counts()` |
| Descriptives | `DESCRIPTIVES VARIABLES=age salary` | `df[['age', 'salary']].describe()` |
| Crosstabs | `CROSSTABS /TABLES=dept BY gender` | `pd.crosstab(df['dept'], df['gender'])` |
| Means by group | `MEANS TABLES=salary BY department` | `df.groupby('department')['salary'].mean()` |

**Pandas Example:**

```python
# Frequencies
print(df['Gender'].value_counts())
print(df['Gender'].value_counts(normalize=True) * 100)  # Percentages

# Descriptive statistics
print(df[['Number_of_children', 'People_in_Household']].describe())

# Crosstabs
crosstab = pd.crosstab(df['Gender'], df['People_in_Household'])
print(crosstab)

# Mean by group
print(df.groupby('Gender')['weight'].mean())
```

### Statistical Tests

| Test | SPSS | Python (scipy/statsmodels) |
|------|------|----------------------------|
| t-test | `T-TEST GROUPS=gender(0 1) /VARIABLES=salary` | `stats.ttest_ind(group1, group2)` |
| Chi-square | `CROSSTABS ... /STATISTICS=CHISQ` | `chi2, p, dof, expected = chi2_contingency(crosstab)` |
| Correlation | `CORRELATIONS /VARIABLES=age salary` | `df[['age', 'salary']].corr()` |
| ANOVA | `ONEWAY salary BY department` | `stats.f_oneway(group1, group2, group3)` |
| Regression | `REGRESSION /DEPENDENT=salary /METHOD=ENTER age experience` | `model = smf.ols('salary ~ age + experience', data=df).fit()` |

**Pandas Example:**

```python
from scipy import stats
import statsmodels.formula.api as smf

# Independent t-test
male = df[df['Gender'] == 'male']['weight']
female = df[df['Gender'] == 'female']['weight']
t_stat, p_value = stats.ttest_ind(male, female)
print(f"t-statistic: {t_stat:.3f}, p-value: {p_value:.3f}")

# Chi-square test
crosstab = pd.crosstab(df['Gender'], df['People_in_Household'])
chi2, p_value, dof, expected = stats.chi2_contingency(crosstab)
print(f"Chi-square: {chi2:.3f}, p-value: {p_value:.3f}")

# Correlation
corr_matrix = df[['age', 'weight']].corr()
print(corr_matrix)
```

### Data Aggregation

| Operation | SPSS | Python (pandas) |
|-----------|------|-----------------|
| Aggregate simple | `AGGREGATE /BREAK=dept /mean_sal=MEAN(salary)` | `df.groupby('dept')['salary'].mean()` |
| Aggregate multiple | `AGGREGATE /BREAK=dept /mean_sal=MEAN(salary) /count=N` | `df.groupby('dept')['salary'].agg(['mean', 'count'])` |
| Add aggregated variable | `AGGREGATE /OUTFILE=* MODE=ADDVARIABLES` | `df['dept_mean'] = df.groupby('dept')['salary'].transform('mean')` |

**Pandas Example:**

```python
# Simple aggregation
dept_avg = df.groupby('People_in_Household')['weight'].mean()
print(dept_avg)

# Multiple aggregations
dept_stats = df.groupby('Gender')['weight'].agg(['mean', 'std', 'count'])
print(dept_stats)

# Add aggregated variable to original dataframe
df['gender_avg_weight'] = df.groupby('Gender')['weight'].transform('mean')
```

### Joining/Merging Data

| Operation | SPSS | Python (pandas) |
|-----------|------|-----------------|
| Match files | `MATCH FILES /FILE=* /TABLE='file2.sav' /BY id` | `pd.merge(df1, df2, on='id', how='left')` |
| Add cases | `ADD FILES /FILE='file1.sav' /FILE='file2.sav'` | `pd.concat([df1, df2], ignore_index=True)` |

**Pandas Example:**

```python
# Read the two sample data files
socio = pd.read_csv("data/socio_demos.csv")
media = pd.read_csv("data/media_contacts.csv")

# Merge on person ID (left join - keep all from socio)
# Note: Column names might differ, so specify left_on and right_on
merged = pd.merge(socio, media, 
                  left_on='Person ID', 
                  right_on='PERSON ID', 
                  how='left')
print(merged.head())
```

---

## Reading SPSS Files in Python

Python can read SPSS `.sav` files directly!

### Using pyreadstat (Recommended)

```python
import pandas as pd
import pyreadstat

# Read SPSS file with metadata
df, meta = pyreadstat.read_sav('data.sav')

# View data
print(df.head())

# View metadata (variable labels, value labels, etc.)
print(meta.column_names_to_labels)
print(meta.variable_value_labels)

# Access variable labels
labels = meta.column_names_to_labels
print(labels)

# Write back with labels preserved
pyreadstat.write_sav(df, 'output.sav',
                     column_labels=labels,
                     variable_value_labels=meta.variable_value_labels)
```

### Using pandas

```python
import pandas as pd

# Read SPSS file (newer versions)
df = pd.read_spss('data.sav')
```

## Common SPSS Procedures in Detail

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

### CROSSTABS with Chi-Square

**SPSS:**

```spss
CROSSTABS
  /TABLES=department BY gender
  /STATISTICS=CHISQ.
```

**Python:**

```python
from scipy.stats import chi2_contingency

# Create crosstab
crosstab = pd.crosstab(df['department'], df['gender'])
print(crosstab)

# Chi-square test
chi2, p_value, dof, expected = chi2_contingency(crosstab)
print(f"Chi-square: {chi2:.3f}")
print(f"p-value: {p_value:.3f}")
print(f"Degrees of freedom: {dof}")
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
print(f"t-statistic: {t_stat:.3f}")
print(f"p-value: {p_value:.3f}")

# With equal_var=False for Welch's t-test
t_stat, p_value = stats.ttest_ind(group1, group2, equal_var=False)
```

### ONEWAY ANOVA with Post-hoc

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
print(f"F-statistic: {f_stat:.3f}")
print(f"p-value: {p_value:.3f}")

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

# Get specific statistics
print(f"R-squared: {model.rsquared:.3f}")
print(f"Adjusted R-squared: {model.rsquared_adj:.3f}")
print("\nCoefficients:")
print(model.params)
print("\np-values:")
print(model.pvalues)
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
from scipy.stats import pearsonr

# Pearson correlation matrix
corr_matrix = df[['age', 'salary', 'experience']].corr()
print(corr_matrix)

# Individual correlation with p-value
r, p = pearsonr(df['age'], df['salary'])
print(f"Correlation: {r:.3f}")
print(f"p-value: {p:.3f}")
```

## Data Transformation Examples

### COMPUTE

**SPSS:**

```spss
COMPUTE total_comp = salary + bonus.
COMPUTE age_squared = age * age.
```

**Python:**

```python
# Create new variables
df['total_comp'] = df['salary'] + df['bonus']
df['age_squared'] = df['age'] ** 2
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

## Visualization

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
import seaborn as sns

# Scatter plot with seaborn
sns.scatterplot(data=df, x='age', y='salary', hue='department')
plt.title('Salary vs Age')
plt.show()
```

## Missing Values

**SPSS:**

```spss
RECODE age (SYSMIS=99).
MISSING VALUES age (99).
```

**Python:**

```python
# Check for missing
print(df.isnull().sum())

# Fill missing with a value
df['age'].fillna(99, inplace=True)

# Drop rows with missing
df_clean = df.dropna()

# Drop columns with any missing
df_clean = df.dropna(axis=1)
```

## Exporting Data

### Export to SPSS

```python
# Save as SPSS file with metadata
pyreadstat.write_sav(df, 'output.sav')
```

### Export to Excel

```python
# Single sheet
df.to_excel('output.xlsx', index=False)

# Multiple sheets
with pd.ExcelWriter('output.xlsx') as writer:
    df.to_excel(writer, sheet_name='Data', index=False)
    summary.to_excel(writer, sheet_name='Summary', index=False)
```

### Export to CSV

```python
df.to_csv('output.csv', index=False)
```

## Pro Tips for SPSS Users

!!! tip "Think in DataFrames"
    In Python, everything is a DataFrame object. Operations are methods: `df.method()`

!!! tip "Use VS Code with Jupyter"
    VS Code + Jupyter extension provides an experience similar to SPSS syntax editor but interactive

!!! tip "Leverage Libraries"
    - **pandas**: Data manipulation (like SPSS data view/variable view)
    - **scipy**: Statistical tests
    - **statsmodels**: Regression and advanced statistics
    - **matplotlib/seaborn**: Graphics

!!! warning "0-based Indexing"
    Python uses 0-based indexing. The first row/column is at position 0.

!!! success "Automation"
    Python excels at automation. One script can process multiple files, generate reports, etc.

## Next Steps

- Work through the [Quick Start Guide](quickstart.md)
- Try the notebooks in the `notebooks/` directory
- Practice with the sample data files in `data/`
- Explore the [Statistical Analysis Tutorial](../tutorials/04-statistical-analysis.md)
- Check the [Cheat Sheets](../reference/cheatsheets.md)

The transition from SPSS to Python opens up powerful new possibilities for your analysis!
