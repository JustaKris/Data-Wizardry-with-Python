# Running Jupyter Notebooks

This guide covers how to work with Jupyter notebooks using **VS Code**, our recommended setup for the team.

## Prerequisites

Before starting, make sure you have:

- ✅ Python installed (see [Installing Python](installing_python.md))
- ✅ uv set up with dependencies installed (see [Using uv](using_uv.md))
- ✅ VS Code installed

## Setting Up VS Code for Jupyter

### Install VS Code

Download from [code.visualstudio.com](https://code.visualstudio.com/) or install via Company Portal.

### Install Required Extensions

Open VS Code and install these extensions:

1. **Python** (by Microsoft) - Python language support
2. **Jupyter** (by Microsoft) - Notebook support in VS Code
3. **Pylance** (by Microsoft) - Advanced Python IntelliSense

**To install:**

- Click the Extensions icon in the sidebar (or press `Ctrl+Shift+X`)
- Search for each extension by name
- Click **Install**

## Opening the Project

1. **Open the project folder**:
   - `File > Open Folder` (or `Ctrl+K Ctrl+O`)
   - Navigate to and select `Data-Wizardry-with-Python`

2. **Select Python interpreter**:
   - Press `Ctrl+Shift+P` to open the Command Palette
   - Type "Python: Select Interpreter"
   - Choose your virtual environment (should show `.venv` or similar)

## Working with Notebooks

### Opening a Notebook

In the VS Code Explorer sidebar:

1. Navigate to the `notebooks/` folder
2. Click any `.ipynb` file to open it
3. The notebook opens directly in VS Code - no browser needed!

### Running Cells

**Multiple ways to run cells:**

- **Click the ▶ play button** next to the cell
- **Press `Shift+Enter`**: Run cell and move to next
- **Press `Ctrl+Enter`**: Run cell and stay on current cell
- **Press `Alt+Enter`**: Run cell and insert new cell below

### Creating a New Notebook

#### Option 1: Via Explorer

1. Right-click in the `notebooks/` folder
2. Select **New File**
3. Name it with `.ipynb` extension (e.g., `my_analysis.ipynb`)

#### Option 2: Via Command Palette

1. Press `Ctrl+Shift+P`
2. Type "Jupyter: Create New Blank Notebook"
3. Save it in the `notebooks/` folder

## VS Code Jupyter Features

### Variable Explorer

View all variables in your notebook:

- Click **Variables** button in the notebook toolbar
- See values, types, and sizes of all variables
- Click any variable to inspect it in detail

### IntelliSense (Code Completion)

As you type, VS Code suggests completions:

- **Methods**: Type `df.` to see all DataFrame methods
- **Variables**: Start typing a variable name for suggestions
- **Imports**: Auto-complete module and function names

Press `Ctrl+Space` to manually trigger suggestions.

### Keyboard Shortcuts

**Command Mode** (press `Esc` to enter):

- `A`: Insert cell above
- `B`: Insert cell below
- `DD`: Delete cell
- `M`: Convert cell to Markdown
- `Y`: Convert cell to Code
- `Z`: Undo cell deletion

**Edit Mode** (press `Enter` on a cell to enter):

- `Ctrl+/`: Comment/uncomment code
- `Tab`: Indent or autocomplete
- `Shift+Tab`: Unindent

**Running Cells**:

- `Shift+Enter`: Run cell, select below
- `Ctrl+Enter`: Run cell, stay on current
- `Alt+Enter`: Run cell, insert below

### Other Useful Features

**Markdown Cells**: Create documentation alongside code

```markdown
# Heading
**bold** and *italic*
- Bullet points
[Links](https://example.com)
```

**Code Folding**: Click arrows next to line numbers to collapse sections

**Multiple Cursors**: `Alt+Click` to add cursors

**Find and Replace**: `Ctrl+F` to search, `Ctrl+H` to replace

## Your First Notebook

Try this in a new notebook:

**Cell 1 (Markdown):**

```markdown
# My First Analysis
Exploring data with pandas
```

**Cell 2 (Code):**

```python
import pandas as pd
import numpy as np

# Create sample data
data = {
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35],
    'Department': ['Sales', 'IT', 'HR']
}

df = pd.DataFrame(data)
df
```

**Cell 3 (Code):**

```python
# Summary statistics
df.describe()
```

Run each cell with `Shift+Enter` and watch the output appear below!

## Tips for Effective Notebook Use

### Organization

- **One concept per cell**: Keep cells focused and small
- **Use Markdown cells**: Document what you're doing and why
- **Clear outputs before committing**: `Ctrl+Shift+P` → "Jupyter: Clear All Outputs"

### Best Practices

- **Restart kernel regularly**: `Ctrl+Shift+P` → "Jupyter: Restart Kernel"
- **Run cells in order**: Avoid running cells out of sequence
- **Save frequently**: `Ctrl+S` saves your notebook
- **Use meaningful names**: `customer_analysis.ipynb` not `untitled1.ipynb`

### Getting Help

In a code cell, you can get help on any function:

```python
# Add ? for quick help
pd.read_csv?

# Or use help()
help(pd.DataFrame)
```

## Troubleshooting

### Kernel Won't Start

1. Make sure your virtual environment is selected as the interpreter
2. Try: `Ctrl+Shift+P` → "Jupyter: Restart Kernel"
3. If that fails, restart VS Code

### Missing Package Error

If you see `ModuleNotFoundError`:

1. Open a terminal in VS Code (`` Ctrl+` ``)
2. Activate the virtual environment if not already active
3. Install the package: `uv pip install package-name`
4. Restart the kernel

### Wrong Python Environment

1. Check the interpreter in the bottom-right of VS Code
2. Press `Ctrl+Shift+P` → "Python: Select Interpreter"
3. Choose the `.venv` environment
4. Restart the kernel

## Alternative: Jupyter Lab (Browser-Based)

If you prefer the traditional browser interface:

1. Open terminal in VS Code (`` Ctrl+` ``)
2. Activate your virtual environment
3. Run:

```bash
jupyter lab
```

Your browser opens to Jupyter Lab. Navigate to `notebooks/` and start working.

**Note**: We recommend VS Code for better Git integration and unified workflow, but Jupyter Lab is available if you prefer it.

## Next Steps

Now you're ready to:

1. **Start learning**: Try the [Quick Start Guide](quickstart.md)
2. **Open a tutorial**: Check `notebooks/01_into_and_data_loading.ipynb`
3. **Explore pandas**: Read the [Pandas Overview](../guides/pandas/overview.md)
