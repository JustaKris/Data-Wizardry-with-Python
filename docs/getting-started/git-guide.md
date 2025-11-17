# Git Guide for Data Analytics

This guide introduces Git version control for colleagues who may be new to it. Git helps you track changes, collaborate with others, and manage your code safely.

## What is Git?

Git is a version control system that:

- **Tracks changes** to your code over time
- **Enables collaboration** with team members
- **Prevents data loss** through history and backups
- **Manages different versions** (branches) of your project

Think of it as "track changes" for code, but much more powerful.

## Installing Git

### Windows

Download from [git-scm.com](https://git-scm.com/download/win) and run the installer.

**Recommended settings during installation:**
- Use Visual Studio Code as Git's default editor
- Override the default branch name: use `main`
- Use bundled OpenSSH
- Use the OpenSSL library
- Checkout Windows-style, commit Unix-style line endings
- Use MinTTY terminal
- Default pull behavior: Fast-forward only

### macOS

```bash
# Using Homebrew (recommended)
brew install git

# Or download from git-scm.com
```

### Linux

```bash
# Debian/Ubuntu
sudo apt-get install git

# Fedora
sudo dnf install git
```

### Verify Installation

```bash
git --version
```

## First-Time Setup

Configure your identity (required for commits):

```bash
# Set your name
git config --global user.name "Your Name"

# Set your email
git config --global user.email "your.email@example.com"

# Set default branch name to 'main'
git config --global init.defaultBranch main

# Set VS Code as default editor
git config --global core.editor "code --wait"
```

## Basic Git Workflow

### 1. Clone a Repository

Download an existing project from GitLab:

```bash
git clone https://gitlab.com/your-org/Data-Wizardry-with-Python.git
cd Data-Wizardry-with-Python
```

### 2. Check Status

See what files have changed:

```bash
git status
```

### 3. Stage Changes

Add files to be committed:

```bash
# Stage a specific file
git add filename.py

# Stage all changes
git add .

# Stage multiple files
git add file1.py file2.py
```

### 4. Commit Changes

Save your staged changes with a message:

```bash
git commit -m "Add data cleaning function"
```

**Good commit messages:**
- "Fix bug in data import"
- "Add visualization for sales trends"
- "Update documentation for installation"

**Bad commit messages:**
- "Update"
- "Changes"
- "asdfasdf"

### 5. Push to Remote

Send your commits to GitLab:

```bash
git push
```

### 6. Pull Latest Changes

Get updates from GitLab:

```bash
git pull
```

## Working with Branches

Branches let you work on features without affecting the main code.

### Create and Switch to a New Branch

```bash
# Create and switch to new branch
git checkout -b feature/new-analysis

# Or in newer Git versions
git switch -c feature/new-analysis
```

### Switch Between Branches

```bash
# Switch to existing branch
git checkout main

# Or in newer Git versions
git switch main
```

### List Branches

```bash
# Local branches
git branch

# All branches (local and remote)
git branch -a
```

### Merge Branches

```bash
# Switch to the branch you want to merge into
git checkout main

# Merge another branch into current branch
git merge feature/new-analysis
```

### Delete a Branch

```bash
# Delete local branch
git branch -d feature/new-analysis

# Force delete (if not merged)
git branch -D feature/new-analysis
```

## Using Git in VS Code

VS Code has excellent built-in Git support. This is the recommended way to use Git for this project.

### Visual Interface

1. **Source Control Panel**: Click the branch icon in the left sidebar (or press `Ctrl+Shift+G`)

2. **See Changes**: Modified files appear in the Source Control panel

3. **Stage Changes**:
   - Hover over a file
   - Click the `+` icon to stage

4. **Commit**:
   - Type a commit message in the text box
   - Press `Ctrl+Enter` or click the checkmark ✓

5. **Push/Pull**:
   - Click the `...` menu in Source Control panel
   - Select "Push" or "Pull"

### VS Code Git Features

- **Diff View**: Click a modified file to see what changed (side-by-side comparison)
- **Inline Annotations**: See who changed each line (GitLens extension recommended)
- **Branch Switching**: Click branch name in bottom-left corner
- **Merge Conflicts**: VS Code highlights conflicts and offers resolution options

### Recommended VS Code Extensions

1. **GitLens** (by GitKraken)
   - Advanced Git visualization
   - Blame annotations
   - Repository history

2. **Git Graph** (by mhutchie)
   - Visual branch graph
   - Easy branch management

To install: `Ctrl+Shift+X` → Search → Install

## Common Git Commands Quick Reference

| Task | Command |
|------|---------|
| Clone repository | `git clone <url>` |
| Check status | `git status` |
| Stage file | `git add <file>` |
| Stage all changes | `git add .` |
| Commit | `git commit -m "message"` |
| Push to remote | `git push` |
| Pull from remote | `git pull` |
| Create branch | `git checkout -b <branch-name>` |
| Switch branch | `git checkout <branch-name>` |
| List branches | `git branch` |
| Merge branch | `git merge <branch-name>` |
| View history | `git log` |
| View history (concise) | `git log --oneline` |
| Discard changes in file | `git checkout -- <file>` |
| Undo last commit (keep changes) | `git reset --soft HEAD~1` |

## Working with GitLab

This repository will be hosted on GitLab. GitLab is similar to GitHub but offers some additional features.

### Key GitLab Concepts

**Repository**: Your project's home on GitLab

**Merge Request (MR)**: Like GitHub's Pull Request - propose changes to be merged

**Issues**: Track bugs, features, and tasks

**CI/CD**: Automated testing and deployment (we'll use this for documentation)

### Creating a Merge Request

1. **Push your branch**:
   ```bash
   git push -u origin feature/your-feature
   ```

2. **In GitLab**:
   - Navigate to your repository
   - Click "Create merge request"
   - Fill in title and description
   - Assign reviewers
   - Click "Create merge request"

3. **After Review**:
   - Address any feedback
   - Push additional commits if needed
   - Once approved, click "Merge"

### Clone from GitLab

```bash
# HTTPS (recommended for beginners)
git clone https://gitlab.com/your-org/Data-Wizardry-with-Python.git

# SSH (after setting up SSH keys)
git clone git@gitlab.com:your-org/Data-Wizardry-with-Python.git
```

### Set Up SSH Keys for GitLab

SSH keys provide secure authentication without passwords.

1. **Generate SSH key**:
   ```bash
   ssh-keygen -t ed25519 -C "your.email@example.com"
   ```
   Press Enter to accept defaults.

2. **Copy public key**:
   ```bash
   # macOS
   pbcopy < ~/.ssh/id_ed25519.pub
   
   # Linux
   cat ~/.ssh/id_ed25519.pub
   
   # Windows (Git Bash)
   cat ~/.ssh/id_ed25519.pub | clip
   ```

3. **Add to GitLab**:
   - Go to GitLab → Settings → SSH Keys
   - Paste your public key
   - Give it a title (e.g., "Work Laptop")
   - Click "Add key"

4. **Test connection**:
   ```bash
   ssh -T git@gitlab.com
   ```

## Best Practices

### Do's

✅ **Commit often**: Small, focused commits are better than large ones

✅ **Write clear commit messages**: Explain what and why

✅ **Pull before you push**: Stay up to date with team changes

✅ **Use branches**: Keep experimental work separate

✅ **Review changes before committing**: Use `git status` and `git diff`

### Don'ts

❌ **Don't commit sensitive data**: No passwords, API keys, or credentials

❌ **Don't commit large files**: Use Git LFS for large datasets (or keep them local)

❌ **Don't work directly on main**: Use feature branches

❌ **Don't force push**: Unless you really know what you're doing

❌ **Don't commit generated files**: Build outputs, `__pycache__`, `.venv`, etc.

## Ignoring Files (.gitignore)

The `.gitignore` file tells Git which files to ignore. Our project already has one that ignores:

```gitignore
# Virtual environments
venv/
.venv/
env/

# Python cache
__pycache__/
*.pyc
*.pyo

# Jupyter
.ipynb_checkpoints/

# IDE
.vscode/
.idea/

# OS files
.DS_Store
Thumbs.db

# Data files (if large)
*.csv
*.xlsx
```

**Note**: The `data/` folder CSV files are tracked because they're small sample files for learning.

## Troubleshooting

### "Permission denied" when pushing

- Check that you have write access to the repository
- Verify your SSH keys are set up correctly
- Try HTTPS instead of SSH

### Merge conflicts

When Git can't automatically merge changes:

1. **VS Code approach** (recommended):
   - Open the conflicted file
   - VS Code highlights conflicts
   - Click "Accept Current Change", "Accept Incoming Change", or "Accept Both Changes"
   - Save the file
   - Stage and commit

2. **Manual approach**:
   ```bash
   # Edit the conflicted file
   # Look for conflict markers: <<<<<<<, =======, >>>>>>>
   # Choose which code to keep
   # Remove conflict markers
   git add <resolved-file>
   git commit -m "Resolve merge conflict"
   ```

### Accidentally committed sensitive data

```bash
# Remove file from Git but keep it locally
git rm --cached sensitive_file.txt

# Add to .gitignore
echo "sensitive_file.txt" >> .gitignore

# Commit the removal
git commit -m "Remove sensitive file from tracking"

# Push
git push
```

**Warning**: This doesn't remove the file from history. For complete removal, contact your GitLab admin.

### Want to undo local changes

```bash
# Discard changes in a specific file
git checkout -- filename.py

# Discard all uncommitted changes (CAREFUL!)
git reset --hard
```

## Learning Resources

- [Git Official Documentation](https://git-scm.com/doc)
- [GitLab Documentation](https://docs.gitlab.com/)
- [VS Code Git Tutorial](https://code.visualstudio.com/docs/sourcecontrol/overview)
- [Interactive Git Tutorial](https://learngitbranching.js.org/)

## Next Steps

Now that you understand Git:

1. ✅ Git installed and configured
2. ✅ Repository cloned
3. ✅ VS Code Git integration ready
4. ✅ Basic workflow understood

Continue with:
- [Installation Guide](installation.md) - Set up Python and dependencies
- [Quick Start Guide](quickstart.md) - Start coding!

---

**Remember**: Git might seem complex at first, but you'll mainly use just a few commands daily. The VS Code integration makes it even easier - you can do most Git operations without touching the command line!
