# Module 6: GitHub CLI (gh) 🚀

## 📖 What is GitHub CLI?

**GitHub CLI** (`gh`) is a command-line tool that brings GitHub functionality to your terminal. It allows you to interact with GitHub repositories, pull requests, issues, and more without leaving the command line.

### Why Use GitHub CLI?
- **Efficiency**: Perform GitHub operations without switching to browser
- **Integration**: Seamlessly integrates with Git workflow
- **Automation**: Script GitHub operations
- **Speed**: Faster than web interface for many tasks
- **Consistency**: Same interface across different platforms

## 🛠️ Installing GitHub CLI

### Windows
```bash
# Using winget
winget install --id GitHub.cli

# Using Chocolatey
choco install gh

# Using Scoop
scoop install gh

# Manual download from https://github.com/cli/cli/releases
```

### macOS
```bash
# Using Homebrew
brew install gh

# Using MacPorts
sudo port install gh
```

### Linux
```bash
# Ubuntu/Debian
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null
sudo apt update
sudo apt install gh

# Fedora/CentOS/RHEL
sudo dnf install gh
```

### GitHub Codespaces
```bash
# GitHub CLI is pre-installed in Codespaces!
gh --version
```

## 🔐 Authentication

Before using GitHub CLI, you need to authenticate:

### Login to GitHub

```bash
# Interactive authentication (recommended)
gh auth login

# Follow the prompts:
# ? What account do you want to log into? GitHub.com
# ? What is your preferred protocol for Git operations? HTTPS/SSH
# ? Authenticate Git with your GitHub credentials? Yes
# ? How would you like to authenticate GitHub CLI? Login with a web browser
```

### Authentication with Token

```bash
# Using personal access token
gh auth login --with-token < token.txt

# Set Git protocol
gh auth setup-git
```

### Check Authentication Status

```bash
# Check current authentication
gh auth status

# List authenticated accounts
gh auth list

# Switch between accounts
gh auth switch
```

## 📁 Repository Management

### Creating Repositories

```bash
# Create public repository
gh repo create my-new-repo --public

# Create private repository
gh repo create my-private-repo --private

# Create repository with description
gh repo create my-app --description "My awesome application"

# Create and clone repository
gh repo create my-project --public --clone

# Create from current directory
gh repo create --source=. --public --push
```

### Repository Operations

```bash
# Clone repository
gh repo clone username/repository-name

# Fork repository
gh repo fork username/repository-name

# Fork and clone
gh repo fork username/repository-name --clone

# View repository
gh repo view username/repository-name

# Edit repository settings
gh repo edit --description "New description"
gh repo edit --visibility private

# Delete repository (careful!)
gh repo delete username/repository-name
```

### Repository Information

```bash
# View repository details
gh repo view

# View in browser
gh repo view --web

# List your repositories
gh repo list

# List user's repositories
gh repo list username

# List organization repositories
gh repo list organization-name
```

## 🔄 Pull Requests

### Creating Pull Requests

```bash
# Create PR interactively
gh pr create

# Create PR with title and body
gh pr create --title "Add new feature" --body "This PR adds a new feature to the application"

# Create PR filling from commits
gh pr create --fill

# Create draft PR
gh pr create --draft

# Create PR to specific branch
gh pr create --base develop

# Create PR with reviewers and assignees
gh pr create --reviewer username1,username2 --assignee username3
```

### Managing Pull Requests

```bash
# List pull requests
gh pr list

# List PRs with filters
gh pr list --state open
gh pr list --author username
gh pr list --label bug

# View PR details
gh pr view 123

# View PR in browser
gh pr view 123 --web

# Check out PR locally
gh pr checkout 123

# Edit PR
gh pr edit 123 --title "New title"
gh pr edit 123 --body "Updated description"
```

### Pull Request Reviews

```bash
# Review PR
gh pr review 123

# Approve PR
gh pr review 123 --approve

# Request changes
gh pr review 123 --request-changes --body "Please fix the formatting"

# Comment on PR
gh pr review 123 --comment --body "Looks good overall"

# View review status
gh pr status
```

### Merging Pull Requests

```bash
# Merge PR with merge commit
gh pr merge 123 --merge

# Squash and merge
gh pr merge 123 --squash

# Rebase and merge
gh pr merge 123 --rebase

# Merge with auto-delete branch
gh pr merge 123 --squash --delete-branch

# Merge when checks pass
gh pr merge 123 --auto --squash
```

## 🐛 Issues Management

### Creating Issues

```bash
# Create issue interactively
gh issue create

# Create issue with title and body
gh issue create --title "Bug in login" --body "Description of the bug"

# Create issue with labels
gh issue create --title "Feature request" --label enhancement,feature

# Create issue with assignees
gh issue create --title "Fix bug" --assignee username1,username2
```

### Managing Issues

```bash
# List issues
gh issue list

# List with filters
gh issue list --state open
gh issue list --label bug
gh issue list --assignee username

# View issue details
gh issue view 456

# View issue in browser
gh issue view 456 --web

# Edit issue
gh issue edit 456 --title "Updated title"
gh issue edit 456 --add-label urgent

# Close issue
gh issue close 456

# Reopen issue
gh issue reopen 456
```

### Issue Comments

```bash
# Comment on issue
gh issue comment 456 --body "This is a comment"

# Edit comment (requires comment ID)
gh issue comment 456 --edit-last
```

## 🏷️ Releases

### Creating Releases

```bash
# Create release
gh release create v1.0.0

# Create release with notes
gh release create v1.0.0 --notes "Release notes here"

# Create release with assets
gh release create v1.0.0 ./dist/*.zip

# Create pre-release
gh release create v1.0.0-beta --prerelease

# Generate release notes automatically
gh release create v1.0.0 --generate-notes
```

### Managing Releases

```bash
# List releases
gh release list

# View release details
gh release view v1.0.0

# Download release assets
gh release download v1.0.0

# Delete release
gh release delete v1.0.0
```

## 👥 Collaboration Features

### Organizations and Teams

```bash
# List organizations
gh org list

# List organization members
gh org list-members organization-name

# List teams in organization
gh team list --org organization-name
```

### Gists

```bash
# Create gist from file
gh gist create file.txt

# Create gist from stdin
echo "Hello World" | gh gist create

# List your gists
gh gist list

# View gist
gh gist view gist-id

# Edit gist
gh gist edit gist-id

# Clone gist
gh gist clone gist-id
```

## 🎯 Workflow Automation

### GitHub Actions

```bash
# List workflow runs
gh run list

# View workflow run details
gh run view run-id

# Watch a workflow run
gh run watch run-id

# Download artifacts
gh run download run-id

# Re-run workflow
gh run rerun run-id
```

### Aliases

Create custom aliases for frequently used commands:

```bash
# Create alias
gh alias set prc 'pr create'
gh alias set prl 'pr list'
gh alias set prv 'pr view'

# Use alias
gh prc --title "My PR"

# List aliases
gh alias list

# Delete alias
gh alias delete prc
```

## 🎯 Complete GitHub CLI Workflow

Let's walk through a complete feature development workflow using GitHub CLI:

### 1. Setup and Repository Creation

```bash
# Authenticate
gh auth login

# Create new repository
gh repo create my-cli-project --public --clone
cd my-cli-project

# Add initial content
echo "# My CLI Project" > README.md
echo "console.log('Hello CLI!');" > app.js
git add .
git commit -m "Initial commit"
git push
```

### 2. Feature Development with Issues

```bash
# Create issue for feature
gh issue create --title "Add user authentication" --body "Need to implement user login and registration" --label feature

# Create feature branch
git checkout -b feature/user-auth

# Work on feature
echo "function login() {}" > auth.js
git add auth.js
git commit -m "Add login function"

echo "function register() {}" >> auth.js
git add auth.js
git commit -m "Add register function"

# Push feature branch
git push -u origin feature/user-auth
```

### 3. Pull Request Creation and Management

```bash
# Create pull request
gh pr create --title "Implement user authentication" --body "This PR implements user login and registration functionality. Closes #1" --reviewer teammate1

# Check PR status
gh pr status

# Make additional changes based on review
echo "function logout() {}" >> auth.js
git add auth.js
git commit -m "Add logout function"
git push

# After approval, merge PR
gh pr merge --squash --delete-branch
```

### 4. Release Management

```bash
# Switch to main and pull latest
git checkout main
git pull

# Create and push tag
git tag v1.0.0
git push --tags

# Create release
gh release create v1.0.0 --generate-notes

# View the release
gh release view v1.0.0
```

## 🔧 Advanced GitHub CLI Features

### Custom Commands with Extensions

```bash
# Install extension
gh extension install owner/gh-extension-name

# List installed extensions
gh extension list

# Create your own extension
gh extension create my-extension
```

### Scripting with GitHub CLI

```bash
#!/bin/bash
# Script to create feature branch and PR

FEATURE_NAME=$1
DESCRIPTION=$2

# Create and switch to feature branch
git checkout -b feature/$FEATURE_NAME

# Make initial commit
echo "# $FEATURE_NAME" > $FEATURE_NAME.md
git add .
git commit -m "Start work on $FEATURE_NAME"

# Push branch
git push -u origin feature/$FEATURE_NAME

# Create draft PR
gh pr create --title "WIP: $FEATURE_NAME" --body "$DESCRIPTION" --draft

echo "Feature branch and draft PR created for $FEATURE_NAME"
```

### Configuration

```bash
# Set default editor
gh config set editor "code --wait"

# Set default protocol
gh config set git_protocol https

# View configuration
gh config list

# Set per-repository settings
gh repo set-default owner/repo
```

## 🎯 Hands-On Exercise

Let's practice a complete GitHub CLI workflow:

### Exercise: Build a Simple Project with Full GitHub Integration

1. **Create and Setup Repository**:
   ```bash
   gh repo create cli-exercise --public --clone
   cd cli-exercise
   ```

2. **Create Project Structure**:
   ```bash
   echo "# CLI Exercise Project" > README.md
   echo "A project to practice GitHub CLI" >> README.md
   
   mkdir src
   echo "console.log('Main app');" > src/app.js
   echo "/* Main styles */" > src/style.css
   
   git add .
   git commit -m "Initial project structure"
   git push
   ```

3. **Create Issue for Feature**:
   ```bash
   gh issue create --title "Add navigation component" --body "Create a navigation component for the application" --label enhancement
   ```

4. **Develop Feature**:
   ```bash
   git checkout -b feature/navigation
   echo "function Navigation() { console.log('Navigation'); }" > src/navigation.js
   git add src/navigation.js
   git commit -m "Add navigation component"
   git push -u origin feature/navigation
   ```

5. **Create Pull Request**:
   ```bash
   gh pr create --title "Add navigation component" --body "Implements navigation component. Closes #1"
   ```

6. **Review and Merge**:
   ```bash
   gh pr view
   gh pr merge --squash --delete-branch
   ```

7. **Create Release**:
   ```bash
   git checkout main
   git pull
   gh release create v0.1.0 --generate-notes
   ```

## 📊 GitHub CLI Commands Summary

| Category | Commands | Description |
|----------|----------|-------------|
| **Auth** | `gh auth login`, `gh auth status` | Authentication management |
| **Repo** | `gh repo create`, `gh repo clone`, `gh repo view` | Repository operations |
| **PR** | `gh pr create`, `gh pr list`, `gh pr merge` | Pull request management |
| **Issues** | `gh issue create`, `gh issue list`, `gh issue close` | Issue management |
| **Releases** | `gh release create`, `gh release list` | Release management |
| **Workflow** | `gh run list`, `gh run view` | GitHub Actions |

## 🚨 Common GitHub CLI Issues and Solutions

### Issue 1: Authentication Problems

```bash
# Problem: Not authenticated or expired token
# Solution: Re-authenticate
gh auth logout
gh auth login
```

### Issue 2: Wrong Repository Context

```bash
# Problem: Commands not working in repository
# Solution: Ensure you're in a Git repository
git remote -v
gh repo set-default owner/repo
```

### Issue 3: Permission Denied

```bash
# Problem: Don't have permissions for repository
# Solution: Check repository access or fork the repository
gh repo fork owner/repo --clone
```

## 📝 GitHub CLI Best Practices

### Do's:
- ✅ Use meaningful commit messages and PR titles
- ✅ Link PRs to issues using "Closes #issue-number"
- ✅ Use draft PRs for work in progress
- ✅ Add reviewers to PRs for code quality
- ✅ Use aliases for frequently used commands

### Don'ts:
- ❌ Force merge PRs without review
- ❌ Create PRs without description
- ❌ Ignore CI/CD check failures
- ❌ Delete repositories without confirmation
- ❌ Share authentication tokens

## 🔗 Integration with Git Commands

GitHub CLI works seamlessly with Git:

```bash
# Traditional workflow
git checkout -b feature/new-feature
git push -u origin feature/new-feature
# Go to GitHub website to create PR

# GitHub CLI workflow
git checkout -b feature/new-feature
git push -u origin feature/new-feature
gh pr create --fill
```

## 📝 Key Takeaways

- **Efficiency**: GitHub CLI speeds up common GitHub operations
- **Integration**: Works seamlessly with existing Git workflow
- **Automation**: Enables scripting of GitHub operations
- **Consistency**: Same interface across all platforms
- **Productivity**: Reduces context switching between terminal and browser

## 🎓 Conclusion

Congratulations! You've now learned:
- Git fundamentals and configuration
- Repository creation and management
- Basic Git workflow (add, commit, push, pull)
- Branch management and switching
- Merging strategies and collaboration
- Advanced GitHub operations with CLI

You're now equipped with the knowledge to use Git and GitHub effectively in your development workflow!

---

**💡 Pro Tip**: Start with basic `gh` commands and gradually incorporate more advanced features. The CLI becomes more powerful as you learn to combine commands and create aliases!
