# Exercise 2: Repository Basics 📁

## 🎯 Objective
Learn to create, initialize, clone, and manage Git repositories using both local and remote operations.

## 📋 Prerequisites
- Completed Exercise 1 (Git Setup)
- Basic terminal/command line knowledge
- GitHub account (for remote operations)

## 🚀 Exercise Tasks

### Task 1: Initialize a Local Repository

1. **Create a new project directory**:
   ```bash
   mkdir my-first-repo
   cd my-first-repo
   ```

2. **Initialize Git repository**:
   ```bash
   git init
   ```

3. **Verify repository creation**:
   ```bash
   ls -la  # Should see .git directory
   git status
   ```

4. **Create initial content**:
   ```bash
   echo "# My First Repository" > README.md
   echo "This is my first Git repository!" >> README.md
   ```

5. **Check repository status**:
   ```bash
   git status
   ```

### Task 2: Make Your First Commit

1. **Add files to staging area**:
   ```bash
   git add README.md
   ```

2. **Check status again**:
   ```bash
   git status
   ```

3. **Create your first commit**:
   ```bash
   git commit -m "Initial commit: Add README"
   ```

4. **View commit history**:
   ```bash
   git log
   git log --oneline
   ```

### Task 3: Clone an Existing Repository

1. **Navigate to parent directory**:
   ```bash
   cd ..
   ```

2. **Clone a public repository** (Octocat's Hello World):
   ```bash
   git clone https://github.com/octocat/Hello-World.git
   ```

3. **Explore the cloned repository**:
   ```bash
   cd Hello-World
   ls -la
   git status
   git log --oneline
   git remote -v
   ```

4. **View repository information**:
   ```bash
   git remote show origin
   ```

### Task 4: Work with Remote Repositories

1. **Go back to your first repository**:
   ```bash
   cd ../my-first-repo
   ```

2. **Add more content**:
   ```bash
   echo "## About This Project" >> README.md
   echo "Learning Git fundamentals step by step." >> README.md
   
   # Create additional files
   echo "print('Hello, Git!')" > script.py
   echo "body { font-family: Arial; }" > style.css
   ```

3. **Add and commit all changes**:
   ```bash
   git add .
   git commit -m "Add project description and initial files"
   ```

4. **View the updated history**:
   ```bash
   git log --oneline
   ```

### Task 5: Repository Inspection

1. **Check repository information**:
   ```bash
   git status
   git branch
   git log --stat
   ```

2. **View file differences**:
   ```bash
   # Make a change
   echo "# This is a comment" >> script.py
   
   # See what changed
   git diff
   git status
   ```

3. **View committed changes**:
   ```bash
   git add script.py
   git commit -m "Add comment to script.py"
   git show HEAD
   ```

## 🎯 Challenge Tasks

### Challenge 1: Multiple Repositories

1. **Create a second repository**:
   ```bash
   cd ..
   mkdir web-project
   cd web-project
   git init
   ```

2. **Create a simple website structure**:
   ```bash
   mkdir css python images
   echo "<!DOCTYPE html><html><head><title>My Site</title></head><body><h1>Hello World</h1></body></html>" > index.html
   echo "h1 { color: blue; }" > css/style.css
   echo "print('Page loaded')" > python/app.py
   echo "# Web Project" > README.md
   ```

3. **Add and commit everything**:
   ```bash
   git add .
   git commit -m "Initial website structure"
   ```

### Challenge 2: Repository Comparison

1. **Compare your repositories**:
   ```bash
   # From web-project directory
   cd ../my-first-repo
   git log --oneline
   echo "---"
   cd ../web-project
   git log --oneline
   ```

2. **Create a summary file**:
   ```bash
   cd ..
   echo "# Repository Summary" > repos-summary.md
   echo "" >> repos-summary.md
   echo "## my-first-repo" >> repos-summary.md
   echo "- Commits: $(cd my-first-repo && git rev-list --count HEAD)" >> repos-summary.md
   echo "- Files: $(cd my-first-repo && git ls-files | wc -l)" >> repos-summary.md
   echo "" >> repos-summary.md
   echo "## web-project" >> repos-summary.md
   echo "- Commits: $(cd web-project && git rev-list --count HEAD)" >> repos-summary.md
   echo "- Files: $(cd web-project && git ls-files | wc -l)" >> repos-summary.md
   
   cat repos-summary.md
   ```

### Challenge 3: Clone Different Repository Types

1. **Clone with specific directory name**:
   ```bash
   git clone https://github.com/octocat/Hello-World.git hello-world-copy
   ```

2. **Clone only specific branch** (if repository has multiple branches):
   ```bash
   git clone -b main https://github.com/octocat/Hello-World.git hello-main-only
   ```

3. **Shallow clone** (recent history only):
   ```bash
   git clone --depth 1 https://github.com/octocat/Hello-World.git hello-shallow
   ```

## 🧪 Practical Scenarios

### Scenario 1: Joining an Existing Project

You've been asked to contribute to an existing project:

1. **Clone the project**:
   ```bash
   # Replace with actual repository URL
   git clone https://github.com/octocat/Hello-World.git project-contribution
   cd project-contribution
   ```

2. **Explore the project structure**:
   ```bash
   find . -type f -name "*.md" -o -name "*.txt" | head -10
   git log --oneline -10
   ```

3. **Check the repository status**:
   ```bash
   git status
   git remote -v
   git branch -a
   ```

### Scenario 2: Starting a Documentation Project

Create a documentation repository:

1. **Initialize and structure**:
   ```bash
   mkdir project-docs
   cd project-docs
   git init
   
   mkdir docs
   mkdir examples
   ```

2. **Create documentation files**:
   ```bash
   echo "# Project Documentation" > README.md
   echo "Welcome to our project documentation!" >> README.md
   
   echo "# Getting Started" > docs/getting-started.md
   echo "# API Reference" > docs/api.md
   echo "# Examples" > docs/examples.md
   
   echo "print('Hello World')" > examples/hello.py
   echo "print('Another example')" > examples/demo.py
   ```

3. **Commit everything**:
   ```bash
   git add .
   git commit -m "Initial documentation structure"
   
   # View the structure
   git ls-files
   tree . 2>/dev/null || find . -type f | grep -v '.git'
   ```

## ✅ Verification Checklist

After completing the exercise, verify your work:

- [ ] Created and initialized a local repository
- [ ] Made commits with meaningful messages
- [ ] Successfully cloned an existing repository
- [ ] Can navigate between repositories
- [ ] Understand the difference between local and remote repositories
- [ ] Can view repository status and history

## 🔍 Knowledge Check

Answer these questions based on your experience:

1. **What does `git init` do?**
   - Creates a new Git repository in the current directory

2. **What's the difference between `git clone` and `git init`?**
   - `git init` creates a new repository; `git clone` copies an existing one

3. **What does the `.git` directory contain?**
   - All Git metadata, history, and configuration for the repository

4. **What happens when you `git clone` a repository?**
   - Downloads all files, history, and sets up remote connection

## 🐛 Troubleshooting

### Issue: "fatal: not a git repository"
**Solution**: You're not in a Git repository directory
```bash
# Check if you're in the right directory
pwd
ls -la | grep .git

# Navigate to correct directory or initialize Git
git init
```

### Issue: Clone fails with permission denied
**Solution**: Check repository URL and access permissions
```bash
# Make sure URL is correct and public
# For private repos, ensure you have access
```

### Issue: Can't see `.git` directory
**Solution**: It's hidden by default
```bash
# Show hidden files
ls -la
# or
ls -d .git
```

## 📊 Repository Analysis Exercise

Create a detailed analysis of one of your repositories:

```bash
# Navigate to one of your repositories
cd my-first-repo

# Create analysis file
echo "# Repository Analysis: $(basename $(pwd))" > analysis.md
echo "" >> analysis.md
echo "## Basic Information" >> analysis.md
echo "- Repository path: $(pwd)" >> analysis.md
echo "- Number of commits: $(git rev-list --count HEAD)" >> analysis.md
echo "- Number of files tracked: $(git ls-files | wc -l)" >> analysis.md
echo "- Current branch: $(git branch --show-current)" >> analysis.md
echo "" >> analysis.md
echo "## Recent Commits" >> analysis.md
git log --oneline -5 >> analysis.md
echo "" >> analysis.md
echo "## Files in Repository" >> analysis.md
git ls-files >> analysis.md

cat analysis.md
```

## 🎉 Congratulations!

You've mastered repository basics! You can now:
- Initialize new repositories
- Clone existing repositories
- Navigate between repositories
- Understand repository structure
- View repository information and history

## ➡️ Next Exercise

Ready to learn the Git workflow? Move on to [Exercise 3: Basic Git Workflow](./exercise-03.md) to master add, commit, and push operations!
