# Welcome to Data Wizardry with Python

Welcome to your comprehensive guide for transitioning from R and SPSS to Python!

## About This Project

**Data Wizardry with Python** is an internal training repository designed to help analysts and data scientists make the transition to Python. Whether you're coming from R, SPSS, or are completely new to programming for analytics, this resource will guide you through the essentials.

## Why Python for Analytics?

Python has become one of the most popular languages for data analysis because:

- **Versatile**: Use the same language for data cleaning, analysis, visualization, and deployment
- **Powerful Libraries**: pandas, NumPy, matplotlib, seaborn, and more provide comprehensive functionality
- **Active Community**: Extensive documentation, tutorials, and support
- **Integration**: Works seamlessly with databases, APIs, and web frameworks
- **Free and Open Source**: No licensing costs, transparent development

## What You'll Learn

### Getting Started

- **[Installation Overview](getting-started/01-installation.md)**: Setup requirements and workflow
- **[Installing Python](getting-started/02-python.md)**: Get Python from Company Portal
- **[Using uv](getting-started/03-uv.md)**: Modern package management with uv sync
- **[Running Notebooks](getting-started/04-notebooks.md)**: Work with Jupyter in VS Code
- **[Quickstart](getting-started/05-quickstart.md)**: Your first data analysis

### Core Guides

- **[Python Basics for Analysts](guides/python_basics_for_analysts.md)**: Essential Python concepts
- **[R to Python Guide](guides/r-to-python.md)**: Translation guide for R users
- **[SPSS to Python Guide](guides/spss-to-python.md)**: Translation guide for SPSS users

### pandas Documentation

- **[pandas Overview](guides/pandas/overview.md)**: Comprehensive pandas guide
- **[pandas Cheat Sheet](guides/pandas/cheat_sheet.md)**: Quick reference for common tasks

### Interactive Notebooks

Hands-on tutorials in `notebooks/`:

1. **Introduction & Data Loading** (`01_into_and_data_loading.ipynb`): Read CSV files, inspect DataFrames, understand data types
2. **Selection & Indexing** (`02_selection_and_indexing.ipynb`): Access and filter data efficiently
3. **Cleaning & Transformations** (`03_cleaning_and_transformations.ipynb`): Handle missing values, duplicates, and data quality
4. **Merging & Joining** (`04_merging_and_joining.ipynb`): Combine datasets from multiple sources
5. **GroupBy & Aggregation** (`05_groupby_and_aggregation.ipynb`): Grouping, summarizing, and aggregation
6. **Reshaping & Pivoting** (`06_reshaping_and_pivoting.ipynb`): Reshape data between long and wide formats
7. **Exporting & Saving** (`07_exporting_and_saving.ipynb`): Save results to various formats

### Reference

- **[Cheatsheets](cheatsheets/cheatsheets.md)**: Quick references for NumPy, Matplotlib, and more
- **[Glossary](reference/glossary.md)**: Key terms and concepts
- **[Resources](reference/resources.md)**: External learning materials

## Repository Structure

```text
Data-Wizardry-with-Python/
├── notebooks/          # Jupyter notebooks with hands-on tutorials
│   ├── 01_into_and_data_loading.ipynb
│   ├── 02_selection_and_indexing.ipynb
│   ├── 03_cleaning_and_transformations.ipynb
│   ├── 04_merging_and_joining.ipynb
│   ├── 05_groupby_and_aggregation.ipynb
│   ├── 06_reshaping_and_pivoting.ipynb
│   └── 07_exporting_and_saving.ipynb
├── data/              # Sample datasets
│   ├── media_contacts.csv
│   └── socio_demos.csv
├── docs/              # MkDocs documentation source
│   ├── getting-started/
│   ├── guides/
│   ├── cheatsheets/
│   └── reference/
├── pyproject.toml     # Modern Python project configuration
└── mkdocs.yml         # Documentation configuration
```

## Learning Approach

This training follows a **learn-by-doing** philosophy:

1. **Read**: Documentation explains concepts clearly
2. **Code**: Jupyter notebooks let you practice interactively
3. **Experiment**: Modify examples to deepen understanding
4. **Apply**: Use what you've learned on real data

## Prerequisites

- Basic understanding of data analysis concepts
- Familiarity with spreadsheets or statistical software
- Willingness to learn and experiment!

No prior Python experience is required, but it's helpful if you've programmed before in any language.

## Support and Community

- 📖 Browse the full documentation using the navigation menu
- 💻 Work through the Jupyter notebooks in the `notebooks/` directory
- 🔍 Search for specific topics using the search bar
- 📝 Check the [Glossary](reference/glossary.md) for terminology
- 📊 Use our [Cheatsheets](cheatsheets/cheatsheets.md) for quick reference

Ready to begin your Python journey? Let's get started!

[Get Started →](getting-started/01-installation.md){ .md-button .md-button--primary }
