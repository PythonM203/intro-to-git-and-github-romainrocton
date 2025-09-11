# Git Cheat Sheet 📋

## 🚀 Quick Reference for Git Commands

This cheat sheet provides quick access to essential Git commands for daily development work.

## ⚙️ Git Configuration

```bash
# Set user identity
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Set default branch name
git config --global init.defaultBranch main

# Set default editor
git config --global core.editor "code --wait"

# View configuration
git config --list
git config user.name
```

## 📁 Repository Operations

```bash
# Initialize new repository
git init

# Clone repository
git clone https://github.com/user/repo.git
git clone https://github.com/user/repo.git new-folder-name

# Add remote
git remote add origin https://github.com/user/repo.git

# View remotes
git remote -v

# Change remote URL
git remote set-url origin https://github.com/user/new-repo.git
```

## 📝 Basic Workflow

```bash
# Check status
git status
git status -s  # Short format

# Add files to staging
git add filename.txt
git add .  # Add all files
git add *.js  # Add all JS files
git add -A  # Add all files including deletions

# Commit changes
git commit -m "Commit message"
git commit -am "Add and commit tracked files"
git commit --amend -m "Fix commit message"

# Push changes
git push
git push origin main
git push -u origin branch-name  # Set upstream

# Pull changes
git pull
git pull origin main
git pull --rebase
```

## 🌿 Branch Management

```bash
# List branches
git branch
git branch -a  # All branches
git branch -r  # Remote branches

# Create branch
git branch branch-name
git checkout -b branch-name  # Create and switch
git switch -c branch-name  # Modern syntax

# Switch branches
git checkout branch-name
git switch branch-name
git checkout -  # Switch to previous branch

# Rename branch
git branch -m new-name
git branch -m old-name new-name

# Delete branch
git branch -d branch-name  # Safe delete
git branch -D branch-name  # Force delete
git push origin --delete branch-name  # Delete remote branch
```

## 🔀 Merging

```bash
# Merge branch
git checkout main
git merge feature-branch

# Merge with no fast-forward
git merge --no-ff feature-branch

# Squash merge
git merge --squash feature-branch

# Abort merge
git merge --abort
```

## 📊 Viewing History

```bash
# View commit history
git log
git log --oneline
git log --graph --oneline
git log --stat
git log -p  # Show changes

# View specific commits
git show HEAD
git show commit-hash
git show HEAD~1  # Previous commit

# Compare commits
git diff
git diff --staged
git diff commit1 commit2
git diff branch1..branch2
```

## ↩️ Undoing Changes

```bash
# Unstage files
git reset HEAD filename.txt
git reset  # Unstage all

# Discard working directory changes
git checkout -- filename.txt
git restore filename.txt  # Modern syntax

# Undo commits
git reset --soft HEAD~1  # Keep changes staged
git reset --mixed HEAD~1  # Keep changes unstaged
git reset --hard HEAD~1  # Discard changes

# Revert commits (safe for shared history)
git revert HEAD
git revert commit-hash
```

## 💾 Stashing

```bash
# Stash changes
git stash
git stash push -m "Work in progress"

# List stashes
git stash list

# Apply stash
git stash pop  # Apply and remove
git stash apply  # Apply and keep
git stash apply stash@{0}  # Apply specific stash

# Drop stash
git stash drop
git stash clear  # Clear all stashes
```

## 🔍 Searching

```bash
# Search in files
git grep "search-term"
git grep -n "search-term"  # Show line numbers

# Search in commit messages
git log --grep="bug fix"

# Search in commits
git log -S "function-name"  # Search for additions/deletions
git log -G "regex-pattern"  # Search with regex
```

## 🏷️ Tags

```bash
# Create tags
git tag v1.0.0
git tag -a v1.0.0 -m "Version 1.0.0"

# List tags
git tag
git tag -l "v1.*"

# Push tags
git push origin v1.0.0
git push --tags

# Delete tags
git tag -d v1.0.0
git push origin --delete v1.0.0
```

## 🔄 Rebasing

```bash
# Rebase branch
git checkout feature-branch
git rebase main

# Interactive rebase
git rebase -i HEAD~3

# Continue/abort rebase
git rebase --continue
git rebase --abort
```

## 🍒 Cherry Picking

```bash
# Cherry pick commit
git cherry-pick commit-hash

# Cherry pick range
git cherry-pick start-hash..end-hash

# Cherry pick without committing
git cherry-pick --no-commit commit-hash
```

## 📋 File Operations

```bash
# Track file moves/renames
git mv old-name.txt new-name.txt

# Remove files
git rm filename.txt
git rm --cached filename.txt  # Remove from Git, keep file

# Ignore files
echo "*.log" >> .gitignore
git add .gitignore
```

## 🔧 Advanced Commands

```bash
# Clean untracked files
git clean -n  # Dry run
git clean -f  # Force clean
git clean -fd  # Clean files and directories

# Reflog (command history)
git reflog

# Bisect (find bad commit)
git bisect start
git bisect bad
git bisect good commit-hash

# Archive repository
git archive --format=zip --output=project.zip HEAD
```

## 🌐 Remote Operations

```bash
# Fetch changes
git fetch origin
git fetch --all

# Track remote branch
git checkout -b local-branch origin/remote-branch
git branch -u origin/remote-branch  # Set upstream

# Push new branch
git push -u origin new-branch

# Force push (use carefully!)
git push --force-with-lease
```

## ⚡ Useful Aliases

Add these to your Git configuration:

```bash
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual '!gitk'
git config --global alias.lg 'log --graph --oneline --all'
```

## 🚨 Emergency Commands

```bash
# I committed to the wrong branch
git reset --soft HEAD~1
git stash
git checkout correct-branch
git stash pop

# I need to undo the last commit
git reset --soft HEAD~1  # Keep changes
git reset --hard HEAD~1  # Discard changes

# I pushed the wrong commit
git revert HEAD  # Safe for shared repos
git reset --hard HEAD~1 && git push --force  # If no one pulled yet

# I accidentally deleted a branch
git reflog  # Find the commit
git checkout -b recovered-branch commit-hash

# I need to fix the last commit message
git commit --amend -m "Fixed message"

# I have merge conflicts
git status  # See conflicted files
# Edit files to resolve conflicts
git add resolved-file.txt
git commit
```

## 📈 Git Flow Workflow

```bash
# Initialize git flow
git flow init

# Start feature
git flow feature start feature-name

# Finish feature
git flow feature finish feature-name

# Start release
git flow release start 1.0.0

# Finish release
git flow release finish 1.0.0

# Start hotfix
git flow hotfix start hotfix-name

# Finish hotfix
git flow hotfix finish hotfix-name
```

## 🎯 Best Practices Reminder

### Commit Messages
- **Good**: "Add user authentication with JWT"
- **Bad**: "fix stuff"

### Branch Names
- **Good**: `feature/user-auth`, `bugfix/login-error`, `hotfix/security-patch`
- **Bad**: `test`, `temp`, `my-branch`

### Workflow
1. Pull before starting work
2. Create feature branch
3. Make small, focused commits
4. Push early and often
5. Create pull request
6. Code review
7. Merge and delete branch

---

**💡 Pro Tip**: Use `git status` frequently to understand your repository state!
