# Installation Guide

This guide will help you set up Python and the required tools for data analytics.

## Step 1: Install Python and Package Manager

### Option A: uv (Recommended)

**uv** is a modern, fast Python package and project manager written in Rust. It's significantly faster than pip and handles virtual environments seamlessly.

#### Install uv

**macOS/Linux:**
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

**Windows:**
```powershell
powershell -c "irm https://astral.sh/uv/install.ps1 | iex"
```

**Verify installation:**
```bash
uv --version
```

#### Using uv

uv automatically manages Python versions and virtual environments. Here's how to use it:

**Install Python (if not already installed):**
```bash
uv python install 3.11
```

**Set up the project:**
```bash
# Navigate to your project directory
cd Data-Wizardry-with-Python

# Create a virtual environment and install dependencies
uv venv
uv pip install -r requirements.txt
```

**Activate the virtual environment:**
```bash
# On macOS/Linux:
source .venv/bin/activate

# On Windows:
.venv\Scripts\activate
```

**Quick commands:**
```bash
# Install a package
uv pip install pandas

# Install from requirements.txt
uv pip install -r requirements.txt

# Run Python with uv (without activating venv)
uv run python script.py

# Run Jupyter with uv
uv run jupyter lab
```

### Option B: Standard Python with venv

For a traditional Python setup:

1. Download Python 3.8+ from [python.org/downloads](https://www.python.org/downloads/)
2. Run the installer
   - ✅ Check "Add Python to PATH" (Windows)
3. Verify installation:

   ```bash
   python --version
   pip --version
   ```

### Option C: Anaconda

Anaconda is a Python distribution that includes most data science packages pre-installed. Good for beginners but larger in size.

1. Download Anaconda from [anaconda.com/download](https://www.anaconda.com/download)
2. Run the installer for your operating system
3. Follow the installation wizard (accept defaults)
4. Verify installation:

   ```bash
   conda --version
   python --version
   ```

## Step 2: Clone the Repository

Open your terminal or command prompt:

```bash
git clone https://github.com/JustaKris/Data-Wizardry-with-Python.git
cd Data-Wizardry-with-Python
```

Don't have Git? Download it from [git-scm.com](https://git-scm.com/) or see our [Git Guide](git-guide.md) for detailed setup instructions.

## Step 3: Create a Virtual Environment and Install Dependencies

Virtual environments keep project dependencies isolated.

### Using uv (Recommended)

If you're using uv, it handles virtual environments automatically:

```bash
# Create virtual environment
uv venv

# Activate it
# On Windows:
.venv\Scripts\activate

# On macOS/Linux:
source .venv/bin/activate

# Install dependencies
uv pip install -r requirements.txt
```

Or use uv without activating the environment:

```bash
# Install dependencies (uv manages the venv)
uv pip install -r requirements.txt

# Run commands directly
uv run jupyter lab
uv run python script.py
```

### Using venv (Standard Python)

```bash
# Create virtual environment
python -m venv venv

# Activate it
# On Windows:
venv\Scripts\activate

# On macOS/Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

### Using conda (Anaconda)

```bash
# Create virtual environment
conda create -n analytics-playground python=3.11

# Activate it
conda activate analytics-playground

# Install dependencies
pip install -r requirements.txt
```

## Step 4: Verify Installation

This will install:

- **pandas**: Data manipulation
- **numpy**: Numerical computing
- **matplotlib & seaborn**: Visualization
- **jupyter**: Interactive notebooks
- **scipy & statsmodels**: Statistical analysis
- **mkdocs**: Documentation
- And more...


Test that everything works:

```python
python -c "import pandas, numpy, matplotlib, jupyter; print('Success!')"
```

If you see "Success!" you're ready to go!

## Step 5: Set Up Your IDE

### Visual Studio Code (Recommended)

**VS Code** is a powerful, free editor with excellent Python and Jupyter support. It's our recommended IDE for this course.

#### Install VS Code

Download from [code.visualstudio.com](https://code.visualstudio.com/)

#### Install Required Extensions

After installing VS Code, add these extensions:

1. **Python** (by Microsoft)
   - Provides Python language support, debugging, linting
   
2. **Jupyter** (by Microsoft)
   - Run Jupyter notebooks directly in VS Code
   - No need to launch a separate browser

3. **Pylance** (by Microsoft)
   - Fast, feature-rich language support for Python

**To install extensions:**
- Open VS Code
- Click the Extensions icon (or press `Ctrl+Shift+X`)
- Search for "Python" and install
- Search for "Jupyter" and install
- Search for "Pylance" and install

#### Using Jupyter in VS Code

1. **Open the project folder**: `File > Open Folder` → select `Data-Wizardry-with-Python`

2. **Select Python interpreter**:
   - Press `Ctrl+Shift+P` (or `Cmd+Shift+P` on Mac)
   - Type "Python: Select Interpreter"
   - Choose your virtual environment (`.venv` or `venv`)

3. **Open a Jupyter notebook**:
   - Navigate to `notebooks/` folder
   - Click on any `.ipynb` file
   - The notebook opens directly in VS Code!

4. **Run cells**:
   - Click the play button next to each cell
   - Or use `Shift+Enter`

**Benefits of VS Code for Jupyter:**
- Integrated experience - no browser needed
- Git integration built-in
- IntelliSense (code completion)
- Variable explorer
- Debugging support

### Alternative: Jupyter Lab (Browser-Based)

If you prefer the traditional browser interface:

```bash
jupyter lab
```

Or Jupyter Notebook:

```bash
jupyter notebook
```

Your browser should open automatically to the Jupyter interface.

### Other IDEs

#### PyCharm

- Python-specific IDE
- Community edition is free
- Download: [jetbrains.com/pycharm](https://www.jetbrains.com/pycharm/)

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
- With uv: Use `uv pip install` instead of `pip install`

### Import errors

If you get import errors:

- Make sure your virtual environment is activated
- Try reinstalling: `pip install --force-reinstall -r requirements.txt`
- Check Python version: `python --version` (should be 3.8+)

### VS Code not detecting virtual environment

- Reload VS Code: Press `Ctrl+Shift+P` and type "Reload Window"
- Manually select interpreter: `Ctrl+Shift+P` → "Python: Select Interpreter"
- Ensure the virtual environment is activated in the integrated terminal

## Next Steps

Now that you're set up:

1. ✅ Python installed
2. ✅ Repository cloned
3. ✅ Virtual environment created
4. ✅ Dependencies installed
5. ✅ VS Code configured with Jupyter

Continue to the [Quick Start Guide](quickstart.md) to write your first Python code!

For help with Git and version control, see the [Git Guide](git-guide.md).
