# Exercise 3: Basic Git Workflow 🔄

## 🎯 Objective
Master the fundamental Git workflow: modify files, stage changes, commit, and push to remote repositories.

## 📋 Prerequisites
- Completed Exercise 1 (Git Setup)
- Completed Exercise 2 (Repository Basics)
- GitHub account for remote operations

## 🚀 Exercise Tasks

### Task 1: Understanding the Three States

1. **Create a practice repository**:
   ```bash
   mkdir git-workflow-practice
   cd git-workflow-practice
   git init
   ```

2. **Create initial files**:
   ```bash
   echo "# Workflow Practice" > README.md
   echo "Learning the Git workflow!" > description.txt
   echo "console.log('Hello Git!');" > app.js
   ```

3. **Check the status** (files are untracked):
   ```bash
   git status
   ```

4. **Add files to staging area**:
   ```bash
   git add README.md
   git status  # README.md is now staged
   
   git add description.txt app.js
   git status  # All files are staged
   ```

5. **Commit the changes**:
   ```bash
   git commit -m "Initial project setup with basic files"
   git status  # Working directory is clean
   ```

### Task 2: Working with Modifications

1. **Modify existing files**:
   ```bash
   echo "" >> README.md
   echo "## Features" >> README.md
   echo "- Basic file operations" >> README.md
   echo "- Git workflow practice" >> README.md
   
   echo "This project helps learn Git basics." >> description.txt
   
   echo "function greet() { return 'Hello World!'; }" >> app.js
   ```

2. **Check what changed**:
   ```bash
   git status
   git diff  # See exact changes
   ```

3. **Stage changes selectively**:
   ```bash
   git add README.md
   git status
   
   git diff --staged  # See staged changes
   git diff           # See unstaged changes
   ```

4. **Commit staged changes**:
   ```bash
   git commit -m "Add features section to README"
   git status
   ```

5. **Stage and commit remaining changes**:
   ```bash
   git add .
   git commit -m "Enhance description and add greet function"
   ```

### Task 3: Working with New Files

1. **Create new files**:
   ```bash
   echo "body { font-family: Arial; }" > style.css
   echo "<!DOCTYPE html><html><body><h1>Git Practice</h1></body></html>" > index.html
   
   mkdir docs
   echo "# Documentation" > docs/guide.md
   ```

2. **Check status and add files**:
   ```bash
   git status
   git add style.css index.html
   git add docs/
   git status
   ```

3. **Commit new files**:
   ```bash
   git commit -m "Add CSS, HTML, and documentation"
   ```

### Task 4: Advanced Staging Operations

1. **Make multiple changes**:
   ```bash
   # Modify multiple files
   echo "/* Updated styles */" >> style.css
   echo "<p>Updated content</p>" >> index.html
   echo "Updated description again." >> description.txt
   ```

2. **Use interactive adding**:
   ```bash
   git add -p  # Patch mode - review each change
   # Press 'y' to stage, 'n' to skip, 'q' to quit
   ```

3. **Use selective staging**:
   ```bash
   git add style.css index.html
   git status
   
   git commit -m "Update styles and HTML content"
   
   git add description.txt
   git commit -m "Update project description"
   ```

### Task 5: Viewing History and Changes

1. **View commit history**:
   ```bash
   git log
   git log --oneline
   git log --graph --oneline
   git log --stat
   ```

2. **View specific commits**:
   ```bash
   git show HEAD      # Latest commit
   git show HEAD~1    # Previous commit
   git show HEAD~2    # Two commits ago
   ```

3. **Compare commits**:
   ```bash
   git diff HEAD~2 HEAD  # Compare two commits ago with current
   ```

## 🌐 Working with Remote Repositories

### Task 6: Connect to GitHub

1. **Create repository on GitHub**:
   - Go to GitHub and create new repository named "git-workflow-practice"
   - Don't initialize with README (we already have one)

2. **Add remote origin**:
   ```bash
   git remote add origin https://github.com/YOUR-USERNAME/git-workflow-practice.git
   git remote -v
   ```

3. **Push to GitHub**:
   ```bash
   git push -u origin main
   ```

4. **Verify on GitHub**: Check your repository on GitHub website

### Task 7: Pull and Push Workflow

1. **Make changes locally**:
   ```bash
   echo "## Installation" >> README.md
   echo "Clone this repository to get started." >> README.md
   
   git add README.md
   git commit -m "Add installation instructions"
   ```

2. **Push changes**:
   ```bash
   git push
   ```

3. **Simulate remote changes** (edit file on GitHub website):
   - Go to your GitHub repository
   - Edit README.md directly on GitHub
   - Add a line like "## Contributing" and "Contributions welcome!"
   - Commit the change on GitHub

4. **Pull remote changes**:
   ```bash
   git pull
   git log --oneline
   ```

## 🎯 Challenge Tasks

### Challenge 1: Complex Workflow Simulation

1. **Create a multi-file feature**:
   ```bash
   # Create a calculator feature
   mkdir calculator
   echo "function add(a, b) { return a + b; }" > calculator/math.js
   echo "function subtract(a, b) { return a - b; }" >> calculator/math.js
   echo "# Calculator Module" > calculator/README.md
   echo "Basic math operations" >> calculator/README.md
   
   # Create tests
   mkdir tests
   echo "// Test file for calculator" > tests/math.test.js
   echo "console.log('Testing add function');" >> tests/math.test.js
   ```

2. **Stage and commit incrementally**:
   ```bash
   git add calculator/math.js
   git commit -m "Add basic math functions"
   
   git add calculator/README.md
   git commit -m "Add calculator documentation"
   
   git add tests/
   git commit -m "Add test framework setup"
   ```

3. **Push all changes**:
   ```bash
   git push
   ```

### Challenge 2: Workflow with Mistakes

1. **Make a mistake and fix it**:
   ```bash
   echo "This is a mistake" > mistake.txt
   git add mistake.txt
   git status
   
   # Unstage the file
   git reset HEAD mistake.txt
   git status
   
   # Remove the file
   rm mistake.txt
   ```

2. **Commit wrong message and fix**:
   ```bash
   echo "function multiply(a, b) { return a * b; }" >> calculator/math.js
   git add calculator/math.js
   git commit -m "wrong commit message"
   
   # Fix the commit message
   git commit --amend -m "Add multiply function to calculator"
   ```

### Challenge 3: File Operations

1. **Rename and move files**:
   ```bash
   # Rename file using Git
   git mv description.txt project-description.txt
   git status
   git commit -m "Rename description file for clarity"
   
   # Move file to subdirectory
   mkdir info
   git mv project-description.txt info/
   git status
   git commit -m "Move description to info directory"
   ```

2. **Delete files**:
   ```bash
   # Remove file
   git rm tests/math.test.js
   git status
   git commit -m "Remove incomplete test file"
   
   # Push changes
   git push
   ```

## 🧪 Practical Scenarios

### Scenario 1: Daily Development Workflow

Simulate a typical day of development:

1. **Start of day - pull latest changes**:
   ```bash
   git pull
   ```

2. **Work on feature throughout the day**:
   ```bash
   # Morning work
   echo "function divide(a, b) { return a / b; }" >> calculator/math.js
   git add calculator/math.js
   git commit -m "Add divide function"
   git push
   
   # Afternoon work
   echo "function power(a, b) { return Math.pow(a, b); }" >> calculator/math.js
   git add calculator/math.js
   git commit -m "Add power function"
   git push
   
   # End of day
   echo "## Usage Examples" >> calculator/README.md
   echo "const result = add(5, 3); // returns 8" >> calculator/README.md
   git add calculator/README.md
   git commit -m "Add usage examples to calculator README"
   git push
   ```

### Scenario 2: Working with Conflicts

1. **Create a potential conflict scenario**:
   ```bash
   # Edit a file
   echo "" >> README.md
   echo "## Version" >> README.md
   echo "Version 1.0.0" >> README.md
   git add README.md
   git commit -m "Add version information"
   ```

2. **Before pushing, someone else pushes** (simulate by editing on GitHub):
   - Edit README.md on GitHub
   - Add "## License" and "MIT License" at the end
   - Commit on GitHub

3. **Try to push and resolve**:
   ```bash
   git push  # This might fail
   git pull  # This will merge or show conflicts
   
   # If there are conflicts, resolve them manually
   # Then commit the merge
   git push
   ```

## ✅ Verification Checklist

After completing the exercise, verify your understanding:

- [ ] Can modify files and see changes with `git status` and `git diff`
- [ ] Understand the difference between staged and unstaged changes
- [ ] Can selectively stage files with `git add`
- [ ] Write meaningful commit messages
- [ ] Can view commit history with various `git log` options
- [ ] Successfully connected local repository to GitHub
- [ ] Can push local changes to remote repository
- [ ] Can pull remote changes to local repository

## 🔍 Knowledge Check

Test your understanding:

1. **What are the three states of files in Git?**
   - Untracked, Staged, Committed

2. **What's the difference between `git diff` and `git diff --staged`?**
   - `git diff` shows unstaged changes; `git diff --staged` shows staged changes

3. **What does `git add .` do?**
   - Stages all modified and new files in the current directory and subdirectories

4. **When should you use `git push -u origin main`?**
   - First time pushing to set up upstream tracking

## 📊 Workflow Summary

Create a summary of your workflow practice:

```bash
# Create workflow summary
echo "# Git Workflow Practice Summary" > workflow-summary.md
echo "" >> workflow-summary.md
echo "## Repository Statistics" >> workflow-summary.md
echo "- Total commits: $(git rev-list --count HEAD)" >> workflow-summary.md
echo "- Total files: $(git ls-files | wc -l)" >> workflow-summary.md
echo "- Repository size: $(du -sh .git | cut -f1)" >> workflow-summary.md
echo "" >> workflow-summary.md
echo "## Recent Activity" >> workflow-summary.md
git log --oneline -5 >> workflow-summary.md
echo "" >> workflow-summary.md
echo "## Files in Repository" >> workflow-summary.md
git ls-files >> workflow-summary.md

# Commit the summary
git add workflow-summary.md
git commit -m "Add workflow practice summary"
git push
```

## 🐛 Common Issues and Solutions

### Issue: Accidentally staged wrong files
```bash
# Unstage specific file
git reset HEAD filename.txt

# Unstage all files
git reset HEAD
```

### Issue: Want to undo last commit (but keep changes)
```bash
git reset --soft HEAD~1
```

### Issue: Want to see what will be pushed
```bash
git log origin/main..HEAD --oneline
```

### Issue: Pushed wrong commit
```bash
# If no one else has pulled yet
git reset --hard HEAD~1
git push --force

# Better approach: revert the commit
git revert HEAD
git push
```

## 🎉 Congratulations!

You've mastered the basic Git workflow! You now understand:
- The three states of files in Git
- How to stage changes selectively
- Writing good commit messages
- Working with remote repositories
- The daily development workflow

## ➡️ Next Exercise

Ready to learn about branching? Move on to [Exercise 4: Branch Management](./exercise-04.md) to learn how to work with multiple parallel development lines!
