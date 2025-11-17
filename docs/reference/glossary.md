# Glossary

## A

**Array**: A NumPy data structure for homogeneous data. The foundation for pandas Series and DataFrame.

**Axis**: Dimension in a DataFrame. `axis=0` refers to rows (down), `axis=1` refers to columns (across).

## B

**Boolean Indexing**: Filtering data using True/False conditions, e.g., `df[df['age'] > 25]`.

**Broadcasting**: NumPy's method of performing operations on arrays of different shapes.

## C

**Column**: Vertical dimension in a DataFrame, representing a variable or feature.

**Crosstab**: Cross-tabulation showing frequency distribution of variables (like a contingency table).

## D

**DataFrame**: pandas' primary 2-dimensional labeled data structure with columns of potentially different types.

**Dependency Group**: Optional dependencies in `pyproject.toml` for specific use cases (e.g., `[dev]`, `[docs]`).

**dtype**: Data type of a column (int64, float64, object, etc.).

## F

**Function**: Reusable block of code that performs a specific task.

**f-string**: Formatted string literal in Python, e.g., `f"Hello {name}"`.

## G

**GroupBy**: Operation that splits data, applies a function, and combines results.

## I

**iloc**: Integer-location based indexing in pandas (position-based).

**Index**: Row labels in a DataFrame or Series.

**Indexing**: Accessing specific elements, rows, or columns in a data structure.

## J

**Join**: Combining DataFrames based on common columns or indices.

**Jupyter Notebook**: Interactive computational environment for creating notebook documents.

## L

**Lambda Function**: Anonymous function defined with `lambda` keyword, e.g., `lambda x: x * 2`.

**List**: Ordered, mutable collection of items in Python.

**List Comprehension**: Concise way to create lists, e.g., `[x**2 for x in range(10)]`.

**loc**: Label-based indexing in pandas (label-based).

## M

**Merge**: Combining DataFrames similar to SQL joins.

**Method**: Function that belongs to an object, called with dot notation, e.g., `df.head()`.

**Method Chaining**: Calling multiple methods in sequence, e.g., `df.filter().sort().head()`.

## N

**NaN**: "Not a Number", pandas' marker for missing numerical data.

**None**: Python's null value.

**NumPy**: Numerical Python library, the foundation for pandas.

## P

**pandas**: Python Data Analysis Library, primary tool for data manipulation.

**PEP 621**: Python Enhancement Proposal defining project metadata format in `pyproject.toml`.

**Pivot Table**: Reshaping tool that summarizes data using aggregation.

**pyproject.toml**: Modern Python project configuration file (dependencies, metadata, tool settings).

**Python**: High-level, general-purpose programming language.

## R

**Row**: Horizontal dimension in a DataFrame, representing an observation or record.

## S

**Series**: pandas' 1-dimensional labeled array, can hold any data type.

**Slice**: Extracting a portion of a sequence, e.g., `df[1:5]`.

## T

**Tuple**: Ordered, immutable collection of items in Python.

## U

**uv**: Modern, fast Python package manager written in Rust. Alternative to pip with automatic venv management.

## V

**Vectorization**: Performing operations on entire arrays without explicit loops (faster).

**View**: Reference to original data (changes affect original). Opposite of copy.

## Comparison with Other Tools

### pandas vs R

| pandas | R equivalent |
|--------|--------------|
| DataFrame | data.frame |
| Series | vector |
| .head() | head() |
| .groupby() | group_by() |
| .merge() | merge() / join() |

### pandas vs SPSS

| pandas | SPSS equivalent |
|--------|-----------------|
| pd.read_csv() | GET DATA |
| .describe() | DESCRIPTIVES |
| .value_counts() | FREQUENCIES |
| pd.crosstab() | CROSSTABS |
| groupby().mean() | MEANS |

### Python vs R Syntax

| Concept | Python | R |
|---------|--------|---|
| Assignment | `x = 5` | `x <- 5` or `x = 5` |
| Indexing | 0-based | 1-based |
| Pipe | Method chaining | `%>%` |
| Function call | `function(data)` | `function(data)` |
| Method call | `data.method()` | N/A (uses functions) |
