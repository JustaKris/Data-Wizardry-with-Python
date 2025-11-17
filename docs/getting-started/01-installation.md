# Installation Guide

Get up and running with Python for data analytics. This guide provides an overview of the installation process.

## Quick Start Path

Follow these guides in order:

1. **[Installing Python](02-python.md)** - Get Python and Git via Company Portal
2. **[Using uv](03-uv.md)** - Set up our recommended package manager
3. **[Running Notebooks](04-notebooks.md)** - Configure VS Code for Jupyter notebooks
4. **[Quick Start](05-quickstart.md)** - Your first data analysis

## What You'll Install

### Core Requirements

- **Python 3.11+**: Programming language for data analysis
- **Git**: Version control system
- **uv**: Fast, modern Python package manager
- **VS Code**: Code editor with excellent Jupyter support

### Python Packages

These are installed automatically via `requirements.txt`:

- **pandas**: Data manipulation and analysis
- **numpy**: Numerical computing
- **matplotlib** & **seaborn**: Data visualization
- **jupyter**: Interactive notebooks
- **scipy** & **statsmodels**: Statistical analysis
- **openpyxl**: Excel file support
- **pyreadstat**: SPSS file reading

## Installation Steps

### 1. Install Python & Git

Use **Company Portal** (recommended) or manual installation.

→ See [Installing Python](02-python.md) for details

### 2. Install uv Package Manager

Install uv with pip:

```bash
pip install uv
```

→ See [Using uv](03-uv.md) for details

### 3. Clone the Repository

```bash
git clone https://gitlab.com/your-org/Data-Wizardry-with-Python.git
cd Data-Wizardry-with-Python
```

### 4. Sync Dependencies

Use the modern `uv sync` workflow:

```bash
# Install all dependencies from pyproject.toml
uv sync --all-groups
```

This creates the virtual environment and installs all packages in one command.

### 5. Configure VS Code

Install VS Code and the Python, Jupyter, and Pylance extensions.

→ See [Running Notebooks](04-notebooks.md) for details

## Verification

Test your setup:

```bash
# Activate environment
.venv\Scripts\activate  # Windows
source .venv/bin/activate  # macOS/Linux

# Test imports
python -c "import pandas, numpy, matplotlib, jupyter; print('✓ All packages installed successfully!')"
```

## Common Issues

### "Command not found" errors

- Ensure Python and Git are in your PATH
- Restart your terminal after installation
- See [Installing Python](02-python.md) troubleshooting section

### Sync fails

- Update uv: `pip install --upgrade uv`
- Check internet connection
- See [Using uv](03-uv.md) troubleshooting section

### Jupyter kernel won't start in VS Code

- Verify correct interpreter is selected
- Restart VS Code
- See [Running Notebooks](04-notebooks.md) troubleshooting section

## What's Next?

Once installation is complete:

1. **Learn the basics**: Try the [Quick Start Guide](05-quickstart.md)
2. **Open a notebook**: Navigate to `notebooks/01_into_and_data_loading.ipynb`
3. **Coming from R?**: Check the [R to Python Guide](../guides/r-to-python.md)
4. **Coming from SPSS?**: Check the [SPSS to Python Guide](../guides/spss-to-python.md)

## Getting Help

If you run into issues:

- Check the detailed guides linked above
- Review the [Git Guide](git-guide.md) for Git-specific questions
- Consult the [Glossary](../reference/glossary.md) for terminology
- Ask a colleague who's already set up
