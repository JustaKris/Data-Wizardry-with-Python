# Installing Python

This guide covers installing Python and Git for your analytics work.

## Prerequisites via Company Portal

The recommended way to install Python and Git is through the **Company Portal**:

1. Open **Company Portal** on your machine
2. Search for and install:
   - **Python 3.11** (or latest version available)
   - **Git for Windows** (Windows) or **Git** (macOS/Linux)
3. Verify installations by opening a terminal and running:

```bash
python --version
git --version
```

You should see version numbers for both tools.

## Alternative: Manual Installation

If Company Portal isn't available or doesn't have the version you need:

### Python

**Download and Install:**

1. Go to [python.org/downloads](https://www.python.org/downloads/)
2. Download Python 3.11 or later
3. Run the installer
   - ✅ **Important (Windows)**: Check "Add Python to PATH"
4. Verify installation:

```bash
python --version
```

### Git

**Download and Install:**

1. Go to [git-scm.com](https://git-scm.com/)
2. Download for your operating system
3. Run the installer (accept defaults)
4. Verify installation:

```bash
git --version
```

For detailed Git setup and usage, see the [Git Guide](git-guide.md).

## What About Anaconda?

While Anaconda is a popular Python distribution that includes many data science packages pre-installed, **we recommend using standard Python with uv** for this team. This approach is:

- **Lighter weight**: Smaller download and disk space
- **Faster**: uv is significantly faster than conda
- **More flexible**: Better control over dependencies
- **Industry standard**: More similar to typical Python workflows

If you already have Anaconda installed, you can still use it, but the rest of this guide assumes standard Python + uv.

## Next Steps

Once Python and Git are installed:

1. **Set up uv**: Continue to [Using uv](using_uv.md)
2. **Clone the repository**: See the [Git Guide](git-guide.md)
3. **Configure VS Code**: See [Running Notebooks](running_notebooks.md)
