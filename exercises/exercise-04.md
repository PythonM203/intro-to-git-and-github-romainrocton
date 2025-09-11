# Exercise 4: Branch Management 🌳

## 🎯 Objective
Master Git branching to work on multiple features simultaneously and manage parallel development lines.

## 📋 Prerequisites
- Completed Exercise 1-3
- Understanding of basic Git workflow
- Repository with some commit history

## 🚀 Exercise Tasks

### Task 1: Understanding Branches

1. **Create a practice repository or use existing one**:
   ```bash
   mkdir branch-practice
   cd branch-practice
   git init
   
   # Create initial content
   echo "# Branch Practice Project" > README.md
   echo "Learning Git branching concepts." >> README.md
   echo "console.log('Main application');" > app.js
   
   git add .
   git commit -m "Initial project setup"
   ```

2. **Check current branch information**:
   ```bash
   git branch              # List local branches
   git branch --show-current  # Show current branch
   git status              # Shows current branch
   ```

### Task 2: Creating and Switching Branches

1. **Create your first feature branch**:
   ```bash
   git branch feature/user-login
   git branch  # See the new branch
   ```

2. **Switch to the new branch**:
   ```bash
   git checkout feature/user-login
   git branch  # Notice the asterisk moved
   ```

3. **Create and switch in one command**:
   ```bash
   git checkout -b feature/navigation
   git branch --show-current
   ```

4. **Try the modern syntax** (Git 2.23+):
   ```bash
   git switch -c feature/footer
   git switch main  # Switch back to main
   ```

### Task 3: Working on Feature Branches

1. **Develop the navigation feature**:
   ```bash
   git switch feature/navigation
   
   # Create navigation files
   echo "function showNavigation() {" > navigation.js
   echo "  console.log('Navigation menu');" >> navigation.js
   echo "}" >> navigation.js
   
   echo "/* Navigation styles */" > navigation.css
   echo ".nav { background: #333; }" >> navigation.css
   
   git add .
   git commit -m "Add basic navigation functionality"
   ```

2. **Continue development**:
   ```bash
   echo "function hideNavigation() {" >> navigation.js
   echo "  console.log('Hide navigation');" >> navigation.js
   echo "}" >> navigation.js
   
   echo ".nav-hidden { display: none; }" >> navigation.css
   
   git add .
   git commit -m "Add navigation hide functionality"
   ```

3. **Work on footer feature**:
   ```bash
   git switch feature/footer
   
   echo "function renderFooter() {" > footer.js
   echo "  return '<footer>© 2025 My App</footer>';" >> footer.js
   echo "}" >> footer.js
   
   echo "/* Footer styles */" > footer.css
   echo "footer { text-align: center; }" >> footer.css
   
   git add .
   git commit -m "Add footer component"
   ```

4. **Work on login feature**:
   ```bash
   git switch feature/user-login
   
   echo "function login(username, password) {" > auth.js
   echo "  console.log('Logging in:', username);" >> auth.js
   echo "  // TODO: Implement actual login" >> auth.js
   echo "}" >> auth.js
   
   echo "function logout() {" >> auth.js
   echo "  console.log('User logged out');" >> auth.js
   echo "}" >> auth.js
   
   git add .
   git commit -m "Add login and logout functions"
   ```

### Task 4: Branch Visualization and Management

1. **View all branches and their commits**:
   ```bash
   git branch -v  # Show last commit on each branch
   git log --graph --oneline --all  # Visual representation
   ```

2. **Compare branches**:
   ```bash
   git switch main
   ls  # See files in main
   
   git switch feature/navigation
   ls  # See files in navigation branch
   
   git switch feature/footer
   ls  # See files in footer branch
   ```

3. **See differences between branches**:
   ```bash
   git diff main feature/navigation
   git diff main..feature/navigation  # Alternative syntax
   ```

### Task 5: Merging Branches

1. **Merge navigation feature into main**:
   ```bash
   git switch main
   git merge feature/navigation
   ls  # See navigation files are now in main
   git log --oneline  # See merge commit
   ```

2. **Merge footer feature**:
   ```bash
   git merge feature/footer
   ls  # See all files
   git log --graph --oneline
   ```

3. **Try a fast-forward merge**:
   ```bash
   # First, create a simple branch for fast-forward
   git checkout -b hotfix/typo-fix
   echo "Fixed typo in footer" >> footer.js
   git add footer.js
   git commit -m "Fix typo in footer"
   
   git switch main
   git merge hotfix/typo-fix  # This will be fast-forward
   git log --oneline
   ```

### Task 6: Branch Cleanup

1. **Delete merged branches**:
   ```bash
   git branch -d feature/navigation
   git branch -d feature/footer
   git branch -d hotfix/typo-fix
   ```

2. **Try to delete unmerged branch**:
   ```bash
   git branch -d feature/user-login  # This will fail
   git branch -D feature/user-login  # Force delete
   ```

3. **View remaining branches**:
   ```bash
   git branch
   ```

## 🎯 Advanced Branch Operations

### Task 7: Branch Renaming

1. **Create and rename a branch**:
   ```bash
   git checkout -b feature/user-settings
   echo "User settings functionality" > settings.js
   git add settings.js
   git commit -m "Add user settings"
   
   # Rename the branch
   git branch -m feature/user-preferences
   git branch  # See the new name
   ```

### Task 8: Working with Remote Branches

1. **Push branch to remote** (if you have a GitHub repository):
   ```bash
   # First, connect to a remote (create repo on GitHub first)
   git remote add origin https://github.com/YOUR-USERNAME/branch-practice.git
   
   # Push main branch
   git push -u origin main
   
   # Create and push a feature branch
   git checkout -b feature/remote-test
   echo "Remote branch test" > remote-test.txt
   git add remote-test.txt
   git commit -m "Add remote test file"
   git push -u origin feature/remote-test
   ```

2. **Work with remote branches**:
   ```bash
   git branch -r  # List remote branches
   git branch -a  # List all branches (local and remote)
   ```

### Task 9: Complex Branching Scenario

1. **Create a branching workflow simulation**:
   ```bash
   # Start from main
   git switch main
   
   # Create develop branch
   git checkout -b develop
   echo "Development version" >> README.md
   git add README.md
   git commit -m "Start development branch"
   
   # Create feature branches from develop
   git checkout -b feature/api-integration develop
   echo "API integration code" > api.js
   git add api.js
   git commit -m "Add API integration"
   
   git checkout develop
   git checkout -b feature/ui-improvements develop
   echo "UI improvements" > ui.js
   git add ui.js
   git commit -m "Add UI improvements"
   
   # Merge features back to develop
   git checkout develop
   git merge feature/api-integration
   git merge feature/ui-improvements
   
   # Merge develop to main
   git checkout main
   git merge develop
   ```

## 🧪 Practical Scenarios

### Scenario 1: Bug Fix While Working on Feature

1. **Start working on a feature**:
   ```bash
   git checkout main
   git checkout -b feature/shopping-cart
   echo "Shopping cart functionality" > cart.js
   git add cart.js
   git commit -m "Start shopping cart feature"
   ```

2. **Urgent bug reported - need to fix immediately**:
   ```bash
   # Switch to main and create hotfix
   git checkout main
   git checkout -b hotfix/login-bug
   
   # Fix the bug
   echo "// Fixed login bug" >> app.js
   git add app.js
   git commit -m "Fix critical login bug"
   
   # Merge hotfix to main
   git checkout main
   git merge hotfix/login-bug
   git branch -d hotfix/login-bug
   ```

3. **Return to feature work**:
   ```bash
   git checkout feature/shopping-cart
   
   # Continue working
   echo "function addToCart() {}" >> cart.js
   git add cart.js
   git commit -m "Add addToCart function"
   
   # Update feature branch with latest main (including bug fix)
   git merge main
   ```

### Scenario 2: Experimental Feature

1. **Create experimental branch**:
   ```bash
   git checkout -b experiment/new-algorithm
   echo "Experimental algorithm" > experimental.js
   git add experimental.js
   git commit -m "Try new algorithm approach"
   
   echo "More experimental code" >> experimental.js
   git add experimental.js
   git commit -m "Refine experimental approach"
   ```

2. **Decide experiment failed**:
   ```bash
   git checkout main
   git branch -D experiment/new-algorithm  # Delete without merging
   ```

3. **Create successful experiment**:
   ```bash
   git checkout -b experiment/performance-boost
   echo "Performance optimizations" > performance.js
   git add performance.js
   git commit -m "Add performance optimizations"
   
   # Experiment successful - merge it
   git checkout main
   git merge experiment/performance-boost
   git branch -d experiment/performance-boost
   ```

## 🎯 Challenge Tasks

### Challenge 1: Complex Merge Scenario

1. **Create conflicting changes**:
   ```bash
   # Update README on main
   git checkout main
   echo "" >> README.md
   echo "## Main Features" >> README.md
   echo "- Basic functionality" >> README.md
   git add README.md
   git commit -m "Add features section"
   
   # Create branch and make conflicting change
   git checkout -b feature/readme-update
   git reset --hard HEAD~1  # Go back before the main change
   echo "" >> README.md
   echo "## Key Features" >> README.md
   echo "- Advanced functionality" >> README.md
   git add README.md
   git commit -m "Add different features section"
   
   # Try to merge - this will create a conflict
   git checkout main
   git merge feature/readme-update
   ```

2. **Resolve the conflict**:
   ```bash
   # Edit README.md to resolve conflict
   # Remove conflict markers and choose/combine content
   git add README.md
   git commit -m "Resolve features section conflict"
   ```

### Challenge 2: Branch Strategy Implementation

Implement a Git Flow-like strategy:

1. **Set up branch structure**:
   ```bash
   git checkout main
   git checkout -b develop
   
   # Create feature branches
   git checkout -b feature/user-management develop
   git checkout -b feature/reporting develop
   
   # Create release branch
   git checkout -b release/v1.0 develop
   ```

2. **Work on each branch appropriately**:
   ```bash
   # Work on user management
   git checkout feature/user-management
   echo "User management system" > users.js
   git add users.js
   git commit -m "Add user management"
   
   # Work on reporting
   git checkout feature/reporting
   echo "Reporting system" > reports.js
   git add reports.js
   git commit -m "Add reporting system"
   
   # Merge features to develop
   git checkout develop
   git merge feature/user-management
   git merge feature/reporting
   
   # Prepare release
   git checkout release/v1.0
   git merge develop
   echo "v1.0.0" > VERSION
   git add VERSION
   git commit -m "Prepare v1.0 release"
   
   # Merge release to main and develop
   git checkout main
   git merge release/v1.0
   git tag v1.0.0
   
   git checkout develop
   git merge release/v1.0
   ```

## ✅ Verification Checklist

After completing the exercise, verify your skills:

- [ ] Can create branches with `git branch` and `git checkout -b`
- [ ] Can switch between branches with `git checkout` or `git switch`
- [ ] Understand that each branch has its own file state
- [ ] Can merge branches into main
- [ ] Can delete branches after merging
- [ ] Can rename branches
- [ ] Understand fast-forward vs. three-way merges
- [ ] Can visualize branch history with `git log --graph`

## 🔍 Knowledge Check

Test your understanding:

1. **What happens when you switch branches?**
   - Git updates your working directory to match the branch's state

2. **What's the difference between `git branch name` and `git checkout -b name`?**
   - First creates branch without switching; second creates and switches

3. **When does Git perform a fast-forward merge?**
   - When the target branch hasn't diverged from the feature branch

4. **Why delete branches after merging?**
   - To keep the branch list clean and manageable

## 📊 Branch Analysis

Create a comprehensive branch analysis:

```bash
# Create branch analysis file
echo "# Branch Management Analysis" > branch-analysis.md
echo "" >> branch-analysis.md
echo "## Current Repository State" >> branch-analysis.md
echo "- Current branch: $(git branch --show-current)" >> branch-analysis.md
echo "- Total commits: $(git rev-list --count HEAD)" >> branch-analysis.md
echo "- Total branches created: [Count during exercise]" >> branch-analysis.md
echo "" >> branch-analysis.md
echo "## Branch History Visualization" >> branch-analysis.md
git log --graph --oneline --all >> branch-analysis.md
echo "" >> branch-analysis.md
echo "## Current Files" >> branch-analysis.md
ls -la | grep -v '.git' >> branch-analysis.md

git add branch-analysis.md
git commit -m "Add branch management analysis"
```

## 🎉 Congratulations!

You've mastered Git branching! You now understand:
- How to create and manage branches
- Switching between different development lines
- Merging branches back to main
- Managing branch lifecycle
- Working with complex branching scenarios

## ➡️ Next Exercise

Ready to learn about collaboration and handling conflicts? Move on to [Exercise 5: Collaboration and Merging](./exercise-05.md) to master team development workflows!
