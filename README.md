# Data Wizardry with Python

A comprehensive training repository for colleagues transitioning from R and SPSS to Python. This repository contains hands-on Jupyter notebooks and detailed documentation to help you master Python for data analytics.

## 🎯 Purpose

This repository is designed for:

- **R users** looking to add Python to their toolkit
- **SPSS users** transitioning to open-source analytics
- **Anyone** wanting to learn modern Python data analysis workflows

## 📚 What's Inside

### Interactive Notebooks

Step-by-step tutorials in `notebooks/` covering the full data analysis workflow:

1. **Data Loading** (`01_data_loading.ipynb`) - Read CSV/Excel files into pandas, inspect DataFrames
2. **Data Cleaning** (`02_data_cleaning.ipynb`) - Handle missing values, duplicates, data quality
3. **Exploratory Data Analysis** (`03_eda.ipynb`) - Summarize and visualize your data
4. **Data Manipulation** (`04_data_manipulation.ipynb`) - Filter, transform, reshape data
5. **Advanced Analysis** (`05_advanced_analysis.ipynb`) - Grouping, aggregation, joins
6. **Exporting** (`06_exporting.ipynb`) - Save results to various formats

All notebooks work with the sample datasets in `data/`.

### Sample Data

Practice with real datasets in the `data/` directory:

- `media_contacts.csv` - Media contact information
- `socio_demos.csv` - Demographic data

These files are used throughout the notebook tutorials.

### Comprehensive Documentation

Built with MkDocs and organized for easy learning:

**Getting Started:**

- [01 Installation](docs/getting-started/01-installation.md) - Quick setup guide
- [02 Installing Python](docs/getting-started/02-python.md) - Python and Git via Company Portal
- [03 Using uv](docs/getting-started/03-uv.md) - Modern package management with uv sync
- [04 Running Notebooks](docs/getting-started/04-notebooks.md) - VS Code Jupyter setup
- [05 Quick Start](docs/getting-started/05-quickstart.md) - Your first data analysis
- [Git Guide](docs/getting-started/git-guide.md) - Version control basics

**Guides:**

- [Python Basics for Analysts](docs/guides/python_basics_for_analysts.md) - Core Python for data work
- [pandas Overview](docs/guides/pandas/overview.md) - Complete pandas guide
- [pandas Cheat Sheet](docs/guides/pandas/cheat_sheet.md) - Quick reference
- [R to Python](docs/guides/r-to-python.md) - Translation guide for R users
- [SPSS to Python](docs/guides/spss-to-python.md) - Translation guide for SPSS users

**Reference:**

- [Cheat Sheets](docs/cheatsheets/cheatsheets.md) - Quick references for all libraries
- [Glossary](docs/reference/glossary.md) - Terminology reference
- [Resources](docs/reference/resources.md) - External learning materials

## 🚀 Getting Started

### Quick Setup (Recommended)

1. **Install via Company Portal:**
   - Python 3.11+
   - Git
   - VS Code

2. **Install uv package manager:**

   ```bash
   pip install uv
   ```

3. **Clone this repository:**

   ```bash
   git clone https://gitlab.com/your-org/Data-Wizardry-with-Python.git
   cd Data-Wizardry-with-Python
   ```

4. **Sync dependencies:**

   Using the modern `uv sync` workflow:

   ```bash
   # Install all dependencies from pyproject.toml
   uv sync --all-groups
   ```

   This creates the virtual environment and installs all packages in one command.

5. **Open in VS Code:**
   - `File > Open Folder` → select `Data-Wizardry-with-Python`
   - Select Python interpreter (`Ctrl+Shift+P` → "Python: Select Interpreter" → choose `.venv`)
   - Open any `.ipynb` file from `notebooks/` folder

**Detailed instructions:** See the [Installation Guide](docs/getting-started/01-installation.md)

### Using the Notebooks

**With VS Code (recommended):**

1. Install VS Code and the Python + Jupyter extensions (or get from Company Portal)
2. Open the project folder in VS Code
3. Select your Python interpreter (`.venv`)
4. Open any `.ipynb` file in the `notebooks/` directory
5. Run cells with `Shift+Enter`

See [Running Notebooks](docs/getting-started/04-notebooks.md) for full VS Code setup.

**Alternative - Jupyter Lab:**

```bash
# Activate environment
.venv\Scripts\activate  # Windows
source .venv/bin/activate  # macOS/Linux

# Start Jupyter
jupyter lab
```

Navigate to the `notebooks/` directory and start with `01_data_loading.ipynb`.

### Viewing the Documentation

Build and serve the documentation locally:

```bash
mkdocs serve
```

Then open your browser to `http://127.0.0.1:8000`

## 📖 Learning Path

We recommend following this sequence:

1. **Setup**: [01 Installation](docs/getting-started/01-installation.md) → [03 Using uv](docs/getting-started/03-uv.md) → [04 Running Notebooks](docs/getting-started/04-notebooks.md)
2. **First Steps**: [05 Quick Start](docs/getting-started/05-quickstart.md) for your first analysis
3. **Python Basics**: [Python Basics for Analysts](docs/guides/python_basics_for_analysts.md)
4. **Master pandas**: [pandas Overview](docs/guides/pandas/overview.md)
5. **Practice**: Work through notebooks in order: `01_data_loading.ipynb` → `02_inspection_and_cleaning.ipynb` → etc.
6. **Reference**: Use [pandas Cheat Sheet](docs/guides/pandas/cheat_sheet.md) and [Cheat Sheets](docs/cheatsheets/cheatsheets.md) as needed

**Coming from another tool?**

- R users: Start with [R to Python Guide](docs/guides/r-to-python.md)
- SPSS users: Start with [SPSS to Python Guide](docs/guides/spss-to-python.md)

## 🛠️ What's Installed

This repository uses modern Python packaging with `pyproject.toml`:

**Core dependencies:**

- **pandas**: Data manipulation and analysis
- **numpy**: Numerical computing
- **matplotlib** & **seaborn**: Data visualization
- **jupyter**: Interactive notebooks
- **scipy**: Scientific computing

**Optional groups:**

- **docs**: MkDocs and documentation tools
- **dev**: Testing and linting tools (pytest, black, ruff)
- **ds**: Extra data science packages (statsmodels, scikit-learn)

Install what you need using `uv pip install -e ".[group]"` or install everything with `".[all]"`.

See `pyproject.toml` for the complete list.

## 🤝 Contributing

We welcome contributions! Whether it's:

- Fixing typos or errors
- Adding new tutorials or examples
- Improving explanations
- Sharing feedback

Please feel free to open an issue or submit a merge request on GitLab.

## 📝 License

This project is intended for internal training purposes.

## 🆘 Getting Help

- Check the [Installation Guide](docs/getting-started/installation.md)
- Review the [Quick Start](docs/getting-started/quickstart.md)
- Browse the [pandas Overview](docs/guides/pandas/overview.md)
- Consult the [Cheat Sheets](docs/cheatsheets/cheatsheets.md)
- Review the [Glossary](docs/reference/glossary.md) for terminology
- Check the [Git Guide](docs/getting-started/git-guide.md) for version control questions
- Open an issue for problems or questions

## 🌟 Acknowledgments

This training material builds on the excellent work of the Python, pandas, and Jupyter communities.

---

**Note**: This repository is hosted on GitLab. Update your remote if you have an existing clone:

```bash
git remote set-url origin https://gitlab.com/your-org/Data-Wizardry-with-Python.git
```
