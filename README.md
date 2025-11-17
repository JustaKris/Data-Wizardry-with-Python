# Python Analytics Playground

A comprehensive training repository for colleagues transitioning from R and SPSS to Python and pandas. This repository contains hands-on Jupyter notebooks and detailed documentation to help you master Python for data analytics.

## 🎯 Purpose

This repository is designed for:
- **R users** looking to add Python to their toolkit
- **SPSS users** transitioning to open-source analytics
- **Anyone** wanting to learn modern Python data analysis workflows

## 📚 What's Inside

### Jupyter Notebooks
Interactive tutorials covering:
- Python basics and syntax
- Data manipulation with pandas
- Data visualization with matplotlib and seaborn
- Statistical analysis with scipy and statsmodels
- Real-world analytics workflows

### Sample Data
Practice with real datasets in the `data/` directory:
- `socio_demos.csv` - Demographic information
- `media_contacts.csv` - Media contact data

These files are ready to use in notebooks and exercises!

### Documentation Site
Comprehensive guides built with MkDocs:
- Installation and setup instructions (featuring uv package manager)
- Git guide for version control
- Quickstart guides optimized for VS Code
- Side-by-side comparisons (R vs Python, SPSS vs Python)
- Reference materials and cheat sheets

## 🚀 Getting Started

### Prerequisites
- Python 3.8 or higher
- Git (see our [Git Guide](docs/getting-started/git-guide.md) for installation)

### Installation

1. Clone this repository:
```bash
git clone https://gitlab.com/your-org/Data-Wizardry-with-Python.git
cd Data-Wizardry-with-Python
```

2. Install uv (recommended) or use standard Python:

**Using uv (recommended):**
```bash
# Install uv
curl -LsSf https://astral.sh/uv/install.sh | sh  # macOS/Linux
# or
powershell -c "irm https://astral.sh/uv/install.ps1 | iex"  # Windows

# Create virtual environment and install dependencies
uv venv
uv pip install -r requirements.txt
```

**Using standard Python:**
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
```

### Using the Notebooks

**With VS Code (recommended):**
1. Install VS Code and the Python + Jupyter extensions
2. Open the project folder
3. Select your Python interpreter
4. Open any `.ipynb` file in the `notebooks/` directory

**With Jupyter Lab:**
```bash
jupyter lab
```

Navigate to the `notebooks/` directory and start with `01-introduction.ipynb`.

### Viewing the Documentation

Build and serve the documentation locally:
```bash
mkdocs serve
```

Then open your browser to `http://127.0.0.1:8000`


## 📖 Learning Path

We recommend following this sequence:

1. **Start Here**: Read the [Installation Guide](docs/getting-started/installation.md)
2. **Version Control**: Review the [Git Guide](docs/getting-started/git-guide.md) if new to Git
3. **Setup**: Install Python with uv and set up VS Code
4. **Foundations**: Work through the [Quick Start](docs/getting-started/quickstart.md)
5. **Core Skills**: Complete notebooks in order using the sample data files
6. **Practice**: Try the exercises in each notebook
7. **Reference**: Use the cheat sheets as needed

## 🤝 Contributing

We welcome contributions! Whether it's:
- Fixing typos or errors
- Adding new tutorials
- Improving explanations
- Sharing feedback

Please feel free to open an issue or submit a merge request on GitLab.

## 📝 License

This project is intended for internal training purposes.

## 🆘 Getting Help

- Check the [documentation](https://gitlab.com/your-org/Data-Wizardry-with-Python/)
- Review the [Git Guide](docs/getting-started/git-guide.md) for version control help
- Review the [glossary](docs/reference/glossary.md) for terminology
- Look at the [cheat sheets](docs/reference/cheatsheets.md) for quick reference
- Open an issue for questions or problems

## 🌟 Acknowledgments

This training material builds on the excellent work of the Python, pandas, and Jupyter communities.

---

**Note**: This repository is transitioning to GitLab. Update your remote if you have an existing clone:
```bash
git remote set-url origin https://gitlab.com/your-org/Data-Wizardry-with-Python.git
```
