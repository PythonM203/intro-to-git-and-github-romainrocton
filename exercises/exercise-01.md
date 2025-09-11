# Exercise 1: Git Setup and Configuration 🛠️

## 🎯 Objective
Learn to install, configure, and verify Git setup for development work.

## 📋 Prerequisites
- Access to a terminal/command prompt
- Internet connection

## 🚀 Exercise Tasks

### Task 1: Verify Git Installation

1. **Check if Git is installed**:
   ```bash
   git --version
   ```
   
   **Expected Output**: Something like `git version 2.34.1`
   
   **If Git is not installed**:
   - Windows: Download from https://git-scm.com/download/win
   - macOS: `brew install git`
   - Linux: `sudo apt install git`
   - Codespaces: Git is pre-installed!

### Task 2: Configure Your Identity

1. **Set your name**:
   ```bash
   git config --global user.name "Your Full Name"
   ```

2. **Set your email** (use your GitHub email):
   ```bash
   git config --global user.email "your.email@example.com"
   ```

3. **Verify your configuration**:
   ```bash
   git config --global user.name
   git config --global user.email
   ```

### Task 3: Configure Default Settings

1. **Set default branch name**:
   ```bash
   git config --global init.defaultBranch main
   ```

2. **Configure line endings** (choose based on your OS):
   ```bash
   # Windows
   git config --global core.autocrlf true
   
   # macOS/Linux
   git config --global core.autocrlf input
   ```

3. **Set default editor** (optional):
   ```bash
   # VS Code
   git config --global core.editor "code --wait"
   
   # Or nano (simpler)
   git config --global core.editor nano
   ```

### Task 4: View Complete Configuration

1. **List all Git configuration**:
   ```bash
   git config --list
   ```

2. **View global configuration file**:
   ```bash
   git config --global --list
   ```

### Task 5: Test Git Help System

1. **Get general help**:
   ```bash
   git help
   ```

2. **Get help for a specific command**:
   ```bash
   git help config
   ```

3. **Get quick help**:
   ```bash
   git config -h
   ```

## ✅ Verification Checklist

After completing the exercise, verify your setup:

- [ ] `git --version` shows Git version
- [ ] `git config user.name` shows your name
- [ ] `git config user.email` shows your email
- [ ] `git config init.defaultBranch` shows "main"
- [ ] `git help` command works

## 🎯 Challenge Tasks

### Challenge 1: Configuration Aliases
Create shortcuts for common Git commands:

```bash
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
```

Test your aliases:
```bash
git st  # Should work like 'git status'
```

### Challenge 2: Global .gitignore
Create a global gitignore file for common files:

```bash
# Create global gitignore
touch ~/.gitignore_global

# Configure Git to use it
git config --global core.excludesfile ~/.gitignore_global

# Add common ignore patterns
echo ".DS_Store" >> ~/.gitignore_global
echo "Thumbs.db" >> ~/.gitignore_global
echo "*.tmp" >> ~/.gitignore_global
```

## 🐛 Troubleshooting

### Issue: "git: command not found"
**Solution**: Git is not installed or not in PATH
- Install Git from official website
- Restart terminal after installation

### Issue: Permission denied
**Solution**: Check file permissions
- On Unix systems: `chmod +x git-command`
- Run with appropriate privileges

### Issue: Wrong name/email showing
**Solution**: Reconfigure Git
```bash
git config --global --unset user.name
git config --global --unset user.email
# Then set them again correctly
```

## 📝 Exercise Summary

Create a file called `git-setup-summary.md` with your configuration:

```markdown
# My Git Setup Summary

## Version Information
- Git Version: [YOUR VERSION]
- Operating System: [YOUR OS]

## Configuration
- Name: [YOUR NAME]
- Email: [YOUR EMAIL]
- Default Branch: main
- Editor: [YOUR EDITOR]

## Aliases Created
- git st → git status
- git co → git checkout
- git br → git branch
- git ci → git commit

## Completion Date
[DATE]
```

## 🎉 Congratulations!

You've successfully configured Git for development! This foundation will be essential for all future Git operations.

## ➡️ Next Exercise

Ready for the next challenge? Move on to [Exercise 2: Repository Basics](./exercise-02.md) to start working with repositories!
