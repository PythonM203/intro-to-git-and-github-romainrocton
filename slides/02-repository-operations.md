# Module 2: Repository Operations 📁

## 📖 Understanding Repositories

A **repository** (or "repo") is like a project folder that Git tracks. It contains:
- Your project files
- Complete history of changes
- Branches and tags
- Configuration settings

## 🆕 Creating a New Repository

### Method 1: Initialize a Local Repository

Start a new Git repository in your current directory:

```bash
# Create a new directory for your project
mkdir my-awesome-project
cd my-awesome-project

# Initialize Git repository
git init

# Check the status
git status
```

What happens when you run `git init`:
- Creates a hidden `.git` folder
- Sets up Git tracking for this directory
- Creates the default branch (usually `main`)

### Method 2: Initialize with a Specific Branch Name

```bash
# Initialize with a specific branch name
git init --initial-branch=main
# or shorter
git init -b main
```

### Method 3: Create Repository on GitHub First

1. Go to [GitHub.com](https://github.com)
2. Click the "+" icon → "New repository"
3. Fill in repository details
4. Clone it locally (see cloning section below)

## 📥 Cloning Repositories

**Cloning** creates a local copy of a remote repository.

### Clone a Repository

```bash
# Basic clone
git clone https://github.com/username/repository-name.git

# Clone into a specific directory
git clone https://github.com/username/repository-name.git my-local-folder

# Clone a specific branch
git clone -b branch-name https://github.com/username/repository-name.git
```

### Clone with SSH (More Secure)

First, set up SSH keys with GitHub, then:

```bash
git clone git@github.com:username/repository-name.git
```

### What Happens When You Clone?
- Downloads all project files
- Downloads complete history
- Sets up remote connection to original repository
- Creates a local working directory

## 🍴 Forking Repositories

**Forking** creates your own copy of someone else's repository on GitHub.

### When to Fork?
- Contributing to open source projects
- Creating your own version of a project
- Experimenting with someone else's code

### How to Fork

#### Method 1: Using GitHub Web Interface
1. Go to the repository you want to fork
2. Click the "Fork" button (top right)
3. Choose where to fork it
4. Clone your fork locally

#### Method 2: Using GitHub CLI (gh)
```bash
# Fork a repository
gh repo fork username/repository-name

# Fork and clone in one command
gh repo fork username/repository-name --clone
```

### Working with Forks

```bash
# Clone your fork
git clone https://github.com/YOUR-USERNAME/repository-name.git
cd repository-name

# Add the original repository as upstream
git remote add upstream https://github.com/ORIGINAL-USERNAME/repository-name.git

# Verify remotes
git remote -v
```

Expected output:
```
origin    https://github.com/YOUR-USERNAME/repository-name.git (fetch)
origin    https://github.com/YOUR-USERNAME/repository-name.git (push)
upstream  https://github.com/ORIGINAL-USERNAME/repository-name.git (fetch)
upstream  https://github.com/ORIGINAL-USERNAME/repository-name.git (push)
```

## 🌐 Understanding Remotes

**Remotes** are versions of your repository hosted on the internet or network.

### Common Remote Operations

```bash
# View remotes
git remote -v

# Add a remote
git remote add origin https://github.com/username/repository-name.git

# Change remote URL
git remote set-url origin https://github.com/username/new-repository-name.git

# Remove a remote
git remote remove origin

# Rename a remote
git remote rename origin upstream
```

### Default Remote Names
- **origin**: Your main remote repository (usually your own repo)
- **upstream**: The original repository (when working with forks)

## 📋 Repository Status and Information

### Check Repository Status
```bash
# See current status
git status

# Shorter status format
git status -s
```

### View Repository Information
```bash
# See remote information
git remote -v

# See all branches
git branch -a

# See commit history
git log --oneline

# See repository configuration
git config --list
```

## 🎯 Practical Examples

### Example 1: Start a New Project

```bash
# 1. Create and navigate to project directory
mkdir my-website
cd my-website

# 2. Initialize Git
git init

# 3. Create a README file
echo "# My Awesome Website" > README.md

# 4. Add and commit
git add README.md
git commit -m "Initial commit: Add README"

# 5. Create repository on GitHub (using gh CLI)
gh repo create my-website --public --source=. --push
```

### Example 2: Contribute to Open Source

```bash
# 1. Fork the repository on GitHub (web interface or gh CLI)
gh repo fork microsoft/vscode --clone

# 2. Navigate to the cloned directory
cd vscode

# 3. Add upstream remote
git remote add upstream https://github.com/microsoft/vscode.git

# 4. Verify remotes
git remote -v

# 5. Create a feature branch (we'll cover this in Module 4)
git checkout -b my-feature-branch
```

### Example 3: Clone and Explore

```bash
# 1. Clone a repository
git clone https://github.com/octocat/Hello-World.git

# 2. Navigate into it
cd Hello-World

# 3. Explore the repository
ls -la
git status
git log --oneline
git remote -v
```

## 🔍 Inspecting Repository Contents

### View Files and Directories
```bash
# List all files (including hidden)
ls -la

# See what Git is tracking
git ls-files

# Check .gitignore
cat .gitignore
```

### Understanding .git Directory
```bash
# WARNING: Don't modify these files manually!
ls .git/
```

The `.git` directory contains:
- **HEAD**: Points to current branch
- **refs/**: Branch and tag references
- **objects/**: All your data (commits, trees, blobs)
- **config**: Repository configuration
- **hooks/**: Custom scripts

## ⚠️ Common Pitfalls and Solutions

### Pitfall 1: Cloning into Wrong Directory
```bash
# Problem: Cloned in wrong place
# Solution: Clone into specific directory
git clone https://github.com/user/repo.git ~/Projects/repo
```

### Pitfall 2: Forgetting to Set Upstream
```bash
# Problem: Can't sync with original repository
# Solution: Add upstream remote
git remote add upstream https://github.com/original-user/repo.git
```

### Pitfall 3: Wrong Remote URL
```bash
# Problem: Can't push/pull
# Check current remotes
git remote -v

# Fix the URL
git remote set-url origin https://github.com/correct-user/repo.git
```

## 🎯 Hands-On Exercise

Let's practice repository operations:

1. **Create a new repository**:
   ```bash
   mkdir git-practice
   cd git-practice
   git init
   ```

2. **Create some content**:
   ```bash
   echo "# Git Practice Repository" > README.md
   echo "console.log('Hello, Git!');" > script.js
   ```

3. **Check status**:
   ```bash
   git status
   ```

4. **Clone an existing repository**:
   ```bash
   cd ..
   git clone https://github.com/octocat/Hello-World.git
   cd Hello-World
   ```

5. **Explore the cloned repository**:
   ```bash
   git status
   git log --oneline
   git remote -v
   ```

## 📊 Repository Types Comparison

| Operation | Local Repository | Forked Repository | Cloned Repository |
|-----------|------------------|-------------------|-------------------|
| Creation | `git init` | Fork button/`gh repo fork` | `git clone` |
| Purpose | New project | Contribute/experiment | Work with existing |
| Remote | Add manually | Automatic (origin + upstream) | Automatic (origin) |
| History | Starts fresh | Full history copied | Full history copied |

## 📝 Key Takeaways

- **Initialize**: Use `git init` for new projects
- **Clone**: Use `git clone` to work with existing repositories
- **Fork**: Create your own copy for contributions
- **Remotes**: Understand origin vs upstream
- **Status**: Always check `git status` to understand current state

## ➡️ Next Steps

Now that you can create and manage repositories, let's learn the basic Git workflow in [Module 3: Basic Git Workflow](./03-basic-workflow.md)!

---

**💡 Pro Tip**: Always run `git status` when you're unsure about the current state of your repository. It's your best friend!
