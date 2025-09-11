# Module 3: Basic Git Workflow 🔄

## 📖 The Git Workflow Overview

The basic Git workflow consists of four main steps:

```
1. MODIFY files in working directory
2. ADD changes to staging area
3. COMMIT changes to repository
4. PUSH changes to remote repository
```

Let's master each step!

## 📁 Understanding the Three Areas

### 1. Working Directory
- Where you edit files
- Contains all your project files
- Changes here are **untracked** until staged

### 2. Staging Area (Index)
- Holds changes ready for the next commit
- Like a shopping cart before checkout
- Changes here are **staged** but not yet permanent

### 3. Repository
- Contains committed changes
- Permanent history of your project
- Changes here are **committed** and tracked

## ➕ Adding Files (git add)

The `git add` command moves changes from the working directory to the staging area.

### Basic Add Commands

```bash
# Add a specific file
git add filename.txt

# Add multiple files
git add file1.txt file2.txt file3.txt

# Add all files in current directory
git add .

# Add all files in the repository
git add -A

# Add all modified files (not new files)
git add -u
```


### Add with Patterns

```bash
# Add all .txt files
git add *.txt

# Add all files in a directory
git add src/

# Add all JavaScript files
git add **/*.js
```

## 📸 Committing Changes (git commit)

A **commit** creates a permanent snapshot of your staged changes.

### Basic Commit

```bash
# Commit with inline message
git commit -m "Add user authentication feature"

# Commit with detailed message (opens editor)
git commit
```

### Commit Message Best Practices

#### Good Commit Messages:
```bash
git commit -m "Add user login functionality"
git commit -m "Fix navigation bug on mobile devices"
git commit -m "Update README with installation instructions"
```

#### Bad Commit Messages:
```bash
git commit -m "stuff"
git commit -m "fixed it"
git commit -m "changes"
```

#### Detailed Commit Message Format:
```
Subject line (50 characters or less)

More detailed explanation if needed. Wrap at 72 characters.
- Use bullet points if helpful
- Explain what and why, not how

Fixes #123
```

### Advanced Commit Options

```bash
# Add and commit in one command (for tracked files only)
git commit -am "Quick fix for typo"

# Commit with detailed message
git commit -m "Add feature" -m "This feature allows users to..."

# Amend the last commit (change message or add files)
git commit --amend -m "Corrected commit message"

# Commit with specific author
git commit --author="Name <email@example.com>" -m "Message"
```

## 🚀 Pushing Changes (git push)

**Pushing** uploads your commits to a remote repository.

### Basic Push Commands

```bash
# Push to default remote and branch
git push

# Push to specific remote and branch
git push origin main

# Push and set upstream (first time)
git push -u origin main

# Push all branches
git push --all

# Push tags
git push --tags
```

### Upstream vs Origin revisited 
- `origin`: default name for your remote repository
- `upstream`: typically refers to the original repository you forked from
- When you are the owner, `origin` and `upstream` often point to the same place
- When you are working in another's repository, `upstream` is the original repo, and `origin` is your fork. 
- Cloning a repo sets `origin` automatically to the cloned repo URL, not yours. 
- Cloning a repo does not set `upstream` automatically. You have to add it manually if needed.

### Push Examples

```bash
# First push to a new repository, the -u flag sets the upstream
git push -u origin main

# Regular pushes after that
git push

# Push a specific branch
git push origin feature-branch

# Force push (use with caution!) 
git push --force
```

## ⬇️ Pulling Changes (git pull)

**Pulling** downloads changes from a remote repository and merges them.

### Basic Pull Commands

```bash
# Pull from default remote and branch
git pull

# Pull from specific remote and branch
git pull origin main

# Pull with rebase instead of merge
git pull --rebase

# Pull all branches
git fetch --all
```

- When you want to work on the last version of the code, always pull first!

### Pull vs Fetch

```bash
# Fetch downloads changes but doesn't merge
git fetch origin

# Pull = fetch + merge
git pull origin main
# Equivalent to:
git fetch origin
git merge origin/main
```

## 🔍 Checking Status and History

### View Repository Status

```bash
# Check current status
git status

# Short status format
git status -s

# Show branch and tracking info
git status -b
```

Status symbols in short format:
- `M` = Modified
- `A` = Added
- `D` = Deleted
- `??` = Untracked
- `R` = Renamed

### View Commit History

```bash
# Basic log
git log

# One line per commit
git log --oneline

# Show changes in each commit
git log -p

# Show last n commits
git log -3

# Show commits with graph
git log --graph --oneline

# Show commits by author
git log --author="Your Name"
```

## 🎯 Complete Workflow Example

Let's walk through a complete workflow:

### 1. Start with a Repository

```bash
# Clone or initialize
git clone https://github.com/username/my-project.git
cd my-project

# Or initialize new
mkdir my-project
cd my-project
git init
```

### 2. Make Changes

```bash
# Create/edit files
echo "# My Project" > README.md
echo "console.log('Hello World');" > app.js
mkdir src
echo "body { margin: 0; }" > src/style.css
```

### 3. Check Status

```bash
git status
```

Output:
```
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	README.md
	app.js
	src/

nothing added to commit but untracked files present
```

### 4. Add Files to Staging

```bash
# Add specific files
git add README.md
git add app.js

# Check status again
git status

# Add remaining files
git add src/
```

### 5. Commit Changes

```bash
git commit -m "Initial project setup

- Add README with project description
- Add main JavaScript file
- Add basic CSS styling"
```

### 6. Push to Remote

```bash
# First push (set upstream)
git push -u origin main

# Future pushes
git push
```

## 🔄 Daily Workflow Pattern

Here's a typical daily workflow:

```bash
# Start of day: Pull latest changes
git pull

# Make changes to files
# ... edit files ...

# Check what changed
git status
git diff

# Add changes
git add .

# Commit changes
git commit -m "Implement user profile page"

# Push to remote
git push

# End of day: Ensure everything is pushed
git status
git push
```

## 🛠️ Useful Workflow Commands

### Undoing Changes

```bash
# Unstage a file (remove from staging area)
git reset HEAD filename.txt

# Discard changes in working directory
git checkout -- filename.txt

# Undo last commit (keep changes in working directory)
git reset HEAD~1

# Undo last commit and discard changes
git reset --hard HEAD~1
```

### Viewing Differences

```bash
# See unstaged changes
git diff

# See staged changes
git diff --staged

# Compare two commits
git diff commit1 commit2

# See changes in a specific file
git diff filename.txt
```

### Stashing Changes

```bash
# Temporarily save changes
git stash

# Apply stashed changes
git stash pop

# List stashes
git stash list

# Apply specific stash
git stash apply stash@{0}
```

## 📊 Git States Diagram

```
Working Directory    Staging Area    Repository    Remote Repository
     (edit)              (add)        (commit)        (push)
┌─────────────┐    ┌─────────────┐   ┌──────────┐   ┌──────────────┐
│   file.txt  │───▶│   file.txt  │──▶│ commit 1 │──▶│   origin/    │
│  (modified) │    │  (staged)   │   │ commit 2 │   │     main     │
└─────────────┘    └─────────────┘   │ commit 3 │   └──────────────┘
                                     └──────────┘
```

## 📝 Workflow Checklist

Before each commit, ask yourself:

- [ ] Did I test my changes?
- [ ] Are my commit messages descriptive?
- [ ] Did I include all necessary files?
- [ ] Did I exclude any files that shouldn't be tracked?
- [ ] Are there any sensitive data (passwords, keys) in my commit?

## ⚠️ Common Mistakes and Solutions

### Mistake 1: Committing Too Large Changes
```bash
# Problem: One commit with 50 file changes
# Solution: Break into smaller, logical commits
git add file1.js
git commit -m "Add user authentication"
git add file2.js file3.js
git commit -m "Add user profile functionality"
```

### Mistake 2: Poor Commit Messages
```bash
# Bad
git commit -m "fix"

# Good
git commit -m "Fix login validation to handle empty email field"
```

### Mistake 3: Forgetting to Pull Before Push
```bash
# Always pull first
git pull
# Then push
git push
```

## 📝 Key Takeaways

- **Workflow**: modify → add → commit → push
- **Status**: Always check `git status` before committing
- **Messages**: Write clear, descriptive commit messages
- **Frequency**: Commit early and often
- **Pull First**: Always pull before pushing to avoid conflicts

## ➡️ Next Steps

Now that you've mastered the basic Git workflow, let's learn about branching in [Module 4: Branch Management](./04-branch-management.md)!

---

**💡 Pro Tip**: The key to good Git usage is developing good habits. Make small, frequent commits with clear messages!
