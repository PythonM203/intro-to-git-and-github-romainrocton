# Module 4: Branch Management 🌳

## 📖 What are Branches?

**Branches** are parallel lines of development in Git. Think of them as alternate timelines where you can work on different features without affecting the main codebase.

### Why Use Branches?
- **Isolation**: Work on features without breaking main code
- **Experimentation**: Try new ideas safely
- **Collaboration**: Multiple developers can work simultaneously
- **Organization**: Separate different types of work
- **History**: Keep a clean, organized project history

### Branch Metaphor
Imagine a tree:
- **Trunk (main)**: Stable, production-ready code
- **Branches**: New features, experiments, bug fixes
- **Leaves**: Individual commits on each branch

## 🌿 Understanding Default Branches

### Main vs Master
- **Modern Git**: Uses `main` as default branch
- **Legacy**: Older repositories may use `master`
- **Configuration**: Set your preference globally

```bash
# Set default branch name for new repositories
git config --global init.defaultBranch main
```

## 👀 Viewing Branches

### List Branches

```bash
# List local branches
git branch

# List all branches (local and remote)
git branch -a

# List remote branches only
git branch -r

# Show last commit on each branch
git branch -v

# Show merged/unmerged branches
git branch --merged
git branch --no-merged
```

### Current Branch Information

```bash
# Show current branch
git branch --show-current

# Alternative method
git rev-parse --abbrev-ref HEAD

# Detailed branch information
git status
```

## 🆕 Creating Branches

### Create a New Branch

```bash
# Create a new branch (but stay on current branch)
git branch feature-login

# Create and switch to new branch
git checkout -b feature-login

# Modern way (Git 2.23+)
git switch -c feature-login

# Create branch from specific commit
git branch feature-login abc1234

# Create branch from another branch
git checkout -b feature-login develop
```

### Branch Naming Conventions

Good branch names are descriptive and follow conventions:

```bash
# Feature branches
git checkout -b feature/user-authentication
git checkout -b feature/shopping-cart
git checkout -b feat/responsive-design

# Bug fixes
git checkout -b bugfix/login-error
git checkout -b fix/mobile-navigation
git checkout -b hotfix/security-patch

# Experiments
git checkout -b experiment/new-algorithm
git checkout -b spike/performance-test
```

## 🔄 Switching Between Branches

### Switch Branches

```bash
# Switch to existing branch (traditional)
git checkout branch-name

# Switch to existing branch (modern)
git switch branch-name

# Switch to previous branch
git checkout -
git switch -

# Switch and create if doesn't exist
git checkout -b new-branch
git switch -c new-branch
```

### Before Switching Branches

Always check your status before switching:

```bash
# Check for uncommitted changes
git status

# If you have uncommitted changes, either:
# 1. Commit them
git add .
git commit -m "Work in progress"

# 2. Stash them (stash saves changes for later)
git stash

# 3. Discard them (careful!)
git checkout -- .
```

## 🗑️ Deleting Branches

### Delete Local Branches

```bash
# Delete merged branch (safe)
git branch -d feature-login

# Force delete branch (even if not merged)
git branch -D feature-login

# Delete multiple branches
git branch -d branch1 branch2 branch3
```

### Delete Remote Branches

```bash
# Delete remote branch
git push origin --delete feature-login

# Alternative syntax
git push origin :feature-login
```

## 🎯 Complete Branching Workflow

Let's walk through a typical feature development workflow:

### 1. Start from Main Branch

```bash
# Make sure you're on main
git checkout main

# Pull latest changes
git pull origin main
```

### 2. Create Feature Branch

```bash
# Create and switch to feature branch
git checkout -b feature/user-profile

# Verify you're on the new branch
git branch --show-current
```

### 3. Work on Feature

```bash
# Make changes
echo "User profile functionality" > profile.js

# Add and commit
git add profile.js
git commit -m "Add basic user profile structure"

# Continue working
echo "function getUserProfile() { }" >> profile.js
git add profile.js
git commit -m "Add getUserProfile function"
```

### 4. Push Feature Branch

```bash
# Push branch to remote
git push -u origin feature/user-profile

# Future pushes
git push
```

### 5. Keep Branch Updated (Optional)

```bash
# Switch to main
git checkout main

# Pull latest changes
git pull

# Switch back to feature branch
git checkout feature/user-profile

# Merge or rebase main into feature branch
git merge main
# or
git rebase main
```

### 6. Finish Feature

```bash
# Final commit
git add .
git commit -m "Complete user profile feature"

# Push final changes
git push
```

## 🔄 Advanced Branch Operations

### Rename Branches

```bash
# Rename current branch
git branch -m new-branch-name

# Rename a different branch
git branch -m old-name new-name

# Update remote after renaming
git push origin -u new-branch-name
git push origin --delete old-name
```

### Copy Branches

```bash
# Create new branch from existing branch
git checkout -b new-branch existing-branch

# Copy current branch
git checkout -b backup-branch
```

### Track Remote Branches

```bash
# Set upstream for existing branch
git push -u origin feature-branch

# Track remote branch when switching
git checkout -b local-branch origin/remote-branch

# Set upstream for current branch
git branch -u origin/feature-branch
```

## 📊 Branch Comparison

### Compare Branches

```bash
# See differences between branches
git diff main feature-branch

# See commits unique to feature branch
git log main..feature-branch

# See commits in both branches
git log main...feature-branch

# Show files changed between branches
git diff --name-only main feature-branch
```

### Visualize Branch History

```bash
# Simple graph
git log --graph --oneline

# Detailed graph
git log --graph --pretty=format:'%h -%d %s (%cr) <%an>'

# All branches
git log --graph --oneline --all

# ASCII graph with more detail
git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --all
```

## 🌳 Branch Strategies

### Git Flow
Popular branching model with specific branch types:

```bash
# Main branches
main (production)
develop (integration)

# Supporting branches
feature/feature-name
release/version-number
hotfix/issue-description
```

### GitHub Flow
Simpler model used by GitHub:

```bash
# Only main branch + feature branches
main (production)
feature/feature-name
```

### Example Implementation:

```bash
# GitHub Flow example
git checkout main
git pull
git checkout -b feature/user-settings
# ... work on feature ...
git push -u origin feature/user-settings
# ... create pull request ...
# ... merge and delete branch ...
```

## 🚨 Common Branch Issues and Solutions

### Issue 1: Can't Switch Branches (Uncommitted Changes)

```bash
# Problem: Uncommitted changes prevent branch switch
# Solution 1: Commit changes
git add .
git commit -m "WIP: temporary commit"

# Solution 2: Stash changes
git stash
git checkout other-branch
git stash pop

# Solution 3: Create commit then move it
git add .
git commit -m "WIP"
git checkout other-branch
git cherry-pick previous-branch
```

### Issue 2: Deleted Branch by Mistake

```bash
# Find the commit hash
git reflog

# Recreate branch
git checkout -b recovered-branch commit-hash
```

### Issue 3: Wrong Branch Name

```bash
# Rename local branch
git branch -m correct-name

# Update remote
git push origin -u correct-name
git push origin --delete old-name
```

## 📋 Branch Management Best Practices

### Do's:
- ✅ Use descriptive branch names
- ✅ Keep branches focused on single features
- ✅ Delete merged branches
- ✅ Pull latest main before creating branches
- ✅ Push branches early for backup

### Don'ts:
- ❌ Work directly on main branch
- ❌ Create branches with generic names like "test" or "temp"
- ❌ Let branches become too long-lived
- ❌ Force push to shared branches
- ❌ Leave branches without commits

## 📊 Branch Commands Cheat Sheet

| Command | Description |
|---------|-------------|
| `git branch` | List local branches |
| `git branch -a` | List all branches |
| `git checkout -b name` | Create and switch to branch |
| `git switch -c name` | Create and switch to branch (modern) |
| `git branch -d name` | Delete merged branch |
| `git branch -D name` | Force delete branch |
| `git push -u origin name` | Push and set upstream |
| `git checkout -` | Switch to previous branch |

## 📝 Key Takeaways

- **Isolation**: Branches provide safe development environments
- **Naming**: Use clear, descriptive branch names
- **Workflow**: Create → Work → Push → Merge → Delete
- **Status**: Always check `git status` before switching
- **Cleanup**: Delete merged branches to keep repository tidy

## ➡️ Next Steps

Now that you understand branch management, let's learn about merging and collaboration in [Module 5: Merging and Collaboration](./05-merging-collaboration.md)!

---

**💡 Pro Tip**: Think of branches as cheap and disposable. Create them liberally for experiments and new features!
