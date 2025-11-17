# Installation Guide

This guide will help you set up Python and the required tools for data analytics.

## Step 1: Install Python

### Option A: Anaconda (Recommended for Beginners)

Anaconda is a Python distribution that includes most data science packages pre-installed.

1. Download Anaconda from [anaconda.com/download](https://www.anaconda.com/download)
2. Run the installer for your operating system
3. Follow the installation wizard (accept defaults)
4. Verify installation:
   ```bash
   conda --version
   python --version
   ```

### Option B: Standard Python

If you prefer a lighter installation:

1. Download Python 3.8+ from [python.org/downloads](https://www.python.org/downloads/)
2. Run the installer
   - ✅ Check "Add Python to PATH" (Windows)
3. Verify installation:
   ```bash
   python --version
   pip --version
   ```

## Step 2: Clone the Repository

Open your terminal or command prompt:

```bash
git clone https://github.com/JustaKris/Data-Wizardry-with-Python.git
cd Data-Wizardry-with-Python
```

Don't have Git? Download it from [git-scm.com](https://git-scm.com/)

## Step 3: Create a Virtual Environment

Virtual environments keep project dependencies isolated.

### Using venv (Standard Python)

```bash
# Create virtual environment
python -m venv venv

# Activate it
# On Windows:
venv\Scripts\activate

# On macOS/Linux:
source venv/bin/activate
```

### Using conda (Anaconda)

```bash
# Create virtual environment
conda create -n analytics-playground python=3.11

# Activate it
conda activate analytics-playground
```

## Step 4: Install Dependencies

With your virtual environment activated:

```bash
pip install -r requirements.txt
```

This will install:
- **pandas**: Data manipulation
- **numpy**: Numerical computing
- **matplotlib & seaborn**: Visualization
- **jupyter**: Interactive notebooks
- **scipy & statsmodels**: Statistical analysis
- **mkdocs**: Documentation
- And more...

## Step 5: Verify Installation

Test that everything works:

```python
python -c "import pandas, numpy, matplotlib, jupyter; print('Success!')"
```

If you see "Success!" you're ready to go!

## Step 6: Launch Jupyter

Start Jupyter Lab:

```bash
jupyter lab
```

Or Jupyter Notebook:

```bash
jupyter notebook
```

Your browser should open automatically to the Jupyter interface.

## Troubleshooting

### Command not found

If you get "command not found" errors:

- **Windows**: Make sure Python is added to PATH
- **macOS/Linux**: Try `python3` instead of `python`
- Restart your terminal after installation

### Permission errors

If you get permission errors when installing packages:

- Don't use `sudo` with pip
- Make sure your virtual environment is activated
- Try `pip install --user -r requirements.txt`

### Import errors

If you get import errors:

- Make sure your virtual environment is activated
- Try reinstalling: `pip install --force-reinstall -r requirements.txt`
- Check Python version: `python --version` (should be 3.8+)

## IDE Recommendations

While Jupyter is great for learning, you might also want:

### Visual Studio Code
- Free, powerful editor
- Great Python and Jupyter support
- Download: [code.visualstudio.com](https://code.visualstudio.com/)

### PyCharm
- Python-specific IDE
- Community edition is free
- Download: [jetbrains.com/pycharm](https://www.jetbrains.com/pycharm/)

### Jupyter Lab
- Modern notebook interface
- Already installed with our requirements
- Launch with `jupyter lab`

## Next Steps

Now that you're set up:

1. ✅ Python installed
2. ✅ Repository cloned
3. ✅ Virtual environment created
4. ✅ Dependencies installed
5. ✅ Jupyter working

Continue to the [Quick Start Guide](quickstart.md) to write your first Python code!
