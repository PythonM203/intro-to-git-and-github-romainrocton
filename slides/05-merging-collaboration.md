# Module 5: Merging and Collaboration 🤝

## 📖 Understanding Merging

**Merging** combines changes from different branches into one branch. It's how we integrate completed features back into the main codebase.

### Types of Merges
1. **Fast-forward merge**: Linear history, no merge commit
2. **Three-way merge**: Creates a merge commit
3. **Squash merge**: Combines all commits into one

## 🔀 Fast-Forward Merges

A fast-forward merge happens when the target branch hasn't changed since the feature branch was created.

### Fast-Forward Example

```bash
# Start from main
git checkout main

# Create feature branch
git checkout -b feature/quick-fix

# Make changes and commit
echo "Quick fix implemented" > fix.txt
git add fix.txt
git commit -m "Implement quick fix"

# Switch back to main
git checkout main

# Fast-forward merge
git merge feature/quick-fix
```

Result: No merge commit created, just moves the main pointer forward.

```
Before:  main → A → B
         feature/quick-fix → A → B → C

After:   main → A → B → C
```

## 🔀 Three-Way Merges

When both branches have diverged, Git creates a merge commit.

### Three-Way Merge Example

```bash
# On main branch, make a change
git checkout main
echo "Main branch change" >> README.md
git add README.md
git commit -m "Update README on main"

# Switch to feature branch and make different change
git checkout feature/user-auth
echo "Authentication feature" > auth.js
git add auth.js
git commit -m "Add authentication"

# Merge feature into main
git checkout main
git merge feature/user-auth
```

This creates a merge commit combining both histories:

```
Before:  main → A → B → D
         feature → A → B → C

After:   main → A → B → D → M
                     ↗ C ↗
```

## 🎯 Basic Merge Commands

### Standard Merge

```bash
# Switch to target branch (usually main)
git checkout main

# Merge feature branch
git merge feature-branch

# Merge with custom message
git merge feature-branch -m "Merge feature: user authentication"

# No fast-forward (always create merge commit)
git merge --no-ff feature-branch
```

### Merge Status

```bash
# Check if merge is in progress
git status

# See what branches are merged
git branch --merged

# See what branches are not merged
git branch --no-merged
```

## ⚔️ Handling Merge Conflicts

**Merge conflicts** occur when Git can't automatically combine changes.

### When Conflicts Happen
- Same line modified in both branches
- File deleted in one branch, modified in another
- File renamed in one branch, modified in another

### Conflict Resolution Process

1. **Identify the conflict**:
   ```bash
   git merge feature-branch
   # Output: CONFLICT (content): Merge conflict in filename.txt
   ```

2. **Check status**:
   ```bash
   git status
   # Shows conflicted files
   ```

3. **Open conflicted file**:
   ```
   <<<<<<< HEAD
   Content from current branch (main)
   =======
   Content from feature branch
   >>>>>>> feature-branch
   ```

4. **Resolve manually**:
   ```
   # Remove conflict markers and choose/combine content
   Final resolved content here
   ```

5. **Mark as resolved**:
   ```bash
   git add filename.txt
   ```

6. **Complete the merge**:
   ```bash
   git commit
   ```

### Conflict Resolution Example

```bash
# Create conflict scenario
git checkout main
echo "Main version" > conflict.txt
git add conflict.txt
git commit -m "Add main version"

git checkout -b feature/conflict
echo "Feature version" > conflict.txt
git add conflict.txt
git commit -m "Add feature version"

# Attempt merge
git checkout main
git merge feature/conflict
# CONFLICT!

# View the conflict
cat conflict.txt
```

Output:
```
<<<<<<< HEAD
Main version
=======
Feature version
>>>>>>> feature/conflict
```

Resolve by editing:
```bash
# Edit file to resolve conflict
echo "Combined version from main and feature" > conflict.txt

# Add resolved file
git add conflict.txt

# Complete merge
git commit -m "Resolve conflict in conflict.txt"
```

## 🛠️ Merge Tools

### Built-in Merge Tools

```bash
# Use Git's built-in merge tool
git mergetool

# Configure default merge tool
git config --global merge.tool vimdiff
git config --global merge.tool vscode
```

### Configure VS Code as Merge Tool

```bash
git config --global merge.tool vscode
git config --global mergetool.vscode.cmd 'code --wait $MERGED'
```

### Abort Merge

```bash
# Cancel merge and return to pre-merge state
git merge --abort
```

## 🔄 Alternative Merge Strategies

### Squash Merge

Combines all commits from feature branch into a single commit:

```bash
# Squash merge
git merge --squash feature-branch
git commit -m "Add complete feature: user authentication"
```

Benefits:
- Clean, linear history
- Single commit for entire feature
- Easy to revert entire feature

### Rebase Instead of Merge

```bash
# Rebase feature branch onto main
git checkout feature-branch
git rebase main

# Then fast-forward merge
git checkout main
git merge feature-branch
```

Benefits:
- Linear history
- No merge commits
- Cleaner project history

## 🌐 Collaboration Workflows

### GitHub Flow

The most common workflow for GitHub-based projects:

1. **Create branch from main**
2. **Make changes and commit**
3. **Push branch to GitHub**
4. **Create Pull Request**
5. **Review and discuss**
6. **Merge and delete branch**

### Complete GitHub Flow Example

```bash
# 1. Start from updated main
git checkout main
git pull origin main

# 2. Create feature branch
git checkout -b feature/shopping-cart

# 3. Work on feature
echo "Shopping cart functionality" > cart.js
git add cart.js
git commit -m "Add shopping cart base functionality"

echo "function addToCart() {}" >> cart.js
git add cart.js
git commit -m "Add addToCart function"

# 4. Push to GitHub
git push -u origin feature/shopping-cart

# 5. Create Pull Request (using GitHub CLI)
gh pr create --title "Add shopping cart feature" --body "Implements basic shopping cart functionality with add/remove items"

# 6. After review and approval, merge
gh pr merge --squash

# 7. Clean up
git checkout main
git pull origin main
git branch -d feature/shopping-cart
```

## 🔧 Pull Requests with GitHub CLI

### Creating Pull Requests

```bash
# Create PR with title and body
gh pr create --title "Fix login bug" --body "Fixes issue with login validation"

# Create PR interactively
gh pr create

# Create PR from current branch
gh pr create --fill

# Create draft PR
gh pr create --draft

# Create PR to specific branch
gh pr create --base develop
```

### Managing Pull Requests

```bash
# List all PRs
gh pr list

# View PR details
gh pr view 123

# Check out PR locally
gh pr checkout 123

# Review PR
gh pr review 123 --approve
gh pr review 123 --request-changes --body "Please fix the typo"

# Merge PR
gh pr merge 123 --squash
gh pr merge 123 --merge
gh pr merge 123 --rebase
```

## 👥 Collaborative Development

### Keeping Your Branch Updated

```bash
# Method 1: Merge main into feature branch
git checkout feature-branch
git merge main

# Method 2: Rebase feature branch onto main
git checkout feature-branch
git rebase main

# Method 3: Pull with rebase
git checkout feature-branch
git pull --rebase origin main
```

### Syncing Forks

When working with forks, keep them synchronized:

```bash
# Add upstream remote (original repository)
git remote add upstream https://github.com/original-owner/repo.git

# Fetch upstream changes
git fetch upstream

# Update your main branch
git checkout main
git merge upstream/main

# Push updates to your fork
git push origin main
```

## 🎯 Complete Collaboration Example

Let's simulate a real collaboration scenario:

### Setup: Create Repository

```bash
mkdir collaborative-project
cd collaborative-project
git init
echo "# Collaborative Project" > README.md
git add README.md
git commit -m "Initial commit"

# Simulate remote repository
echo "Repository created!"
```

### Developer A: Add Feature

```bash
# Create feature branch
git checkout -b feature/user-management

# Add feature files
echo "class UserManager {}" > user-manager.js
git add user-manager.js
git commit -m "Add UserManager class"

echo "function createUser() {}" >> user-manager.js
git add user-manager.js
git commit -m "Add createUser function"

# Push feature
git push -u origin feature/user-management
```

### Developer B: Add Different Feature

```bash
# Start from main
git checkout main

# Create different feature
git checkout -b feature/data-validation

# Add feature
echo "function validateEmail() {}" > validation.js
git add validation.js
git commit -m "Add email validation"

# Push feature
git push -u origin feature/data-validation
```

### Integration: Merge Both Features

```bash
# Merge first feature
git checkout main
git merge feature/user-management

# Merge second feature
git merge feature/data-validation

# Push integrated changes
git push origin main

# Clean up branches
git branch -d feature/user-management
git branch -d feature/data-validation
git push origin --delete feature/user-management
git push origin --delete feature/data-validation
```

## 🚨 Common Collaboration Issues

### Issue 1: Merge Conflicts in Pull Requests

```bash
# Update your branch with latest main
git checkout feature-branch
git fetch origin
git merge origin/main

# Resolve conflicts
# ... resolve conflicts manually ...
git add .
git commit -m "Resolve merge conflicts"

# Push updated branch
git push
```

### Issue 2: Outdated Fork

```bash
# Add upstream if not already added
git remote add upstream https://github.com/original/repo.git

# Sync with upstream
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
```

### Issue 3: Accidental Commits to Main

```bash
# Move commits to new branch
git branch feature/accidental-commits
git reset --hard HEAD~3  # Remove last 3 commits from main
git checkout feature/accidental-commits
```

## 📋 Pull Request Best Practices

### Writing Good PR Descriptions

```markdown
## Summary
Brief description of what this PR does.

## Changes
- Add user authentication
- Update login form validation
- Fix password reset bug

## Testing
- [ ] Unit tests pass
- [ ] Manual testing completed
- [ ] No console errors

## Screenshots
(if applicable)

Fixes #123
```

### PR Review Guidelines

**As Author**:
- Keep PRs small and focused
- Write clear descriptions
- Respond to feedback promptly
- Update based on reviews

**As Reviewer**:
- Be constructive and kind
- Test the changes locally
- Check for edge cases
- Approve when satisfied

## 📊 Merge Strategies Comparison

| Strategy | Pros | Cons | When to Use |
|----------|------|------|-------------|
| **Merge Commit** | Preserves history, shows feature branches | Can create complex history | Team prefers full history |
| **Squash Merge** | Clean linear history, easy to revert | Loses individual commit history | Want clean main branch |
| **Rebase Merge** | Linear history, no merge commits | Can be complex, rewrites history | Advanced teams, clean history |

## 📝 Key Takeaways

- **Merge Early**: Integrate changes frequently to avoid large conflicts
- **Small PRs**: Keep pull requests focused and reviewable
- **Communication**: Discuss major changes before implementing
- **Testing**: Always test merged code
- **Clean Up**: Delete merged branches to keep repository tidy

## ➡️ Next Steps

Now that you understand merging and collaboration, let's explore advanced GitHub operations with [Module 6: GitHub CLI](./06-github-cli.md)!

---

**💡 Pro Tip**: The best way to avoid merge conflicts is to communicate with your team and merge/rebase frequently!
