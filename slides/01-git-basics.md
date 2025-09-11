# Module 1: Git Basics 🚀

## 📖 What is Git?

Git is a **distributed version control system** that tracks changes in computer files and coordinates work on those files among multiple people. It's like having a time machine for your code!

### Why Use Version Control?
- **Track Changes**: See what changed, when, and who made the change
- **Backup**: Never lose your work again
- **Collaboration**: Multiple people can work on the same project
- **Branching**: Work on different features simultaneously
- **History**: Go back to any previous version of your code

## 🛠️ Installing Git

### On Windows
```bash
# Download from https://git-scm.com/download/win
# Or use chocolatey (if available)
choco install git

# Verify installation
git --version
```

### On macOS
```bash
# Using Homebrew
brew install git

# Or download from https://git-scm.com/download/mac

# Verify installation
git --version
```

### On Linux (Ubuntu/Debian)
```bash
# Update package list
sudo apt update

# Install Git
sudo apt install git

# Verify installation
git --version
```

### In GitHub Codespaces
```bash
# Git is already installed! Just verify:
git --version
```

## ⚙️ Initial Git Configuration

Before using Git, you need to configure your identity. This information will be attached to your commits.

### Set Your Name and Email
```bash
# Set your name (use your real name)
git config --global user.name "Your Name"

# Set your email (use your GitHub email)
git config --global user.email "your.email@example.com"
```

### Configure Default Branch Name
```bash
# Set default branch name to 'main'
git config --global init.defaultBranch main
```

### Configure Line Endings (Important for cross-platform work)
```bash
# On Windows
git config --global core.autocrlf true

# On macOS/Linux
git config --global core.autocrlf input
```

### Configure Default Editor (Optional)
```bash
# Use VS Code as default editor
git config --global core.editor "code --wait"

# Or use nano (simpler for beginners)
git config --global core.editor nano
```

### View Your Configuration
```bash
# See all configuration
git config --list

# See specific values
git config user.name
git config user.email
```

## 📚 Git Terminology

Let's learn the essential Git vocabulary:

### Repository (Repo)
A **repository** is a directory that contains your project files and the entire history of changes.

### Commit
A **commit** is a snapshot of your project at a specific point in time. Think of it as saving your game progress.

### Working Directory
The **working directory** is where you modify files. It's your current workspace.

### Staging Area (Index)
The **staging area** is where you prepare changes before committing them. It's like a shopping cart before checkout.

### Branch
A **branch** is a parallel version of your repository. The default branch is usually called `main`.

### Remote
A **remote** is a version of your repository hosted on a server (like GitHub).

### Clone
**Cloning** means downloading a repository from a remote server to your local machine.

### Fork
**Forking** creates a personal copy of someone else's repository on GitHub.

## 🎯 The Git Workflow

Understanding the basic Git workflow is crucial:

```
Working Directory → Staging Area → Repository → Remote Repository
      ↓                ↓             ↓           ↓
   Edit files      git add       git commit   git push
```

### The Three States of Files in Git:

1. **Modified**: You've changed the file but haven't committed it yet
2. **Staged**: You've marked a modified file to go into your next commit
3. **Committed**: The data is safely stored in your local repository

## 🔍 Getting Help

Git has excellent built-in help:

```bash
# General help
git help

# Help for specific commands
git help add
git help commit
git help push

# Quick help (shorter version)
git add -h
git commit -h
```

## ✅ Verification Commands

Let's verify everything is set up correctly:

```bash
# Check Git version
git --version

# Check your configuration
git config --list

# Check specific settings
git config user.name
git config user.email
git config init.defaultBranch
```

Expected output should look like:
```
git version 2.34.1
user.name=Your Name
user.email=your.email@example.com
init.defaultbranch=main
```

## 🚨 Common Issues and Solutions

### Issue: Git command not found
**Solution**: Git is not installed or not in your PATH
```bash
# Check if Git is installed
which git
# or
where git
```

### Issue: Permission denied
**Solution**: You might need to configure SSH keys or use HTTPS
```bash
# Check remote URL
git remote -v

# Switch to HTTPS if needed
git remote set-url origin https://github.com/username/repo.git
```

### Issue: Wrong user name/email in commits
**Solution**: Reconfigure Git
```bash
# Fix globally
git config --global user.name "Correct Name"
git config --global user.email "correct.email@example.com"
```

## 🎯 Practice Exercise

Let's practice what we've learned:

1. **Check Git installation**:
   ```bash
   git --version
   ```

2. **Configure your identity**:
   ```bash
   git config --global user.name "Your Name"
   git config --global user.email "your.email@example.com"
   ```

3. **Verify configuration**:
   ```bash
   git config --list
   ```

4. **Get help**:
   ```bash
   git help status
   ```

## 📝 Key Takeaways

- Git is a distributed version control system
- Configuration is essential before first use
- The three main areas: Working Directory, Staging Area, Repository
- Files can be modified, staged, or committed
- Help is always available with `git help`

## ➡️ Next Steps

Now that you have Git configured, let's move to [Module 2: Repository Operations](./02-repository-operations.md) where you'll learn how to create, clone, and fork repositories!

---

**💡 Pro Tip**: Practice these commands multiple times. Muscle memory is important when working with Git!
