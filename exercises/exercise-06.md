# Exercise 6: GitHub CLI Mastery 🚀

## 🎯 Objective
Master the GitHub CLI (gh) to perform advanced GitHub operations directly from the terminal, including repository management, pull requests, issues, and automation.

## 📋 Prerequisites
- Completed Exercises 1-5
- GitHub account with repositories
- GitHub CLI installed (`gh` command)
- Basic understanding of GitHub web interface

## 🛠️ Setup: Install and Authenticate GitHub CLI

### Step 1: Install GitHub CLI

**If not already installed:**

**Windows:**
```bash
winget install --id GitHub.cli
```

**macOS:**
```bash
brew install gh
```

**Linux:**
```bash
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null
sudo apt update
sudo apt install gh
```

**GitHub Codespaces:**
```bash
# GitHub CLI is pre-installed!
gh --version
```

### Step 2: Authenticate

```bash
# Authenticate with GitHub
gh auth login

# Check authentication status
gh auth status
```

## 🚀 Exercise Tasks

### Task 1: Repository Management with GitHub CLI

1. **Create a new repository using gh**:
   ```bash
   # Create public repository
   gh repo create gh-cli-practice --public --description "Learning GitHub CLI operations"
   
   # Clone the repository
   gh repo clone gh-cli-practice
   cd gh-cli-practice
   ```

2. **Set up initial project structure**:
   ```bash
   echo "# GitHub CLI Practice Project" > README.md
   echo "Mastering GitHub operations from the command line." >> README.md
   
   mkdir src docs tests
   echo "print('GitHub CLI App')" > src/app.py
   echo "# Documentation" > docs/README.md
   echo "# Tests" > tests/app_test.py
   
   git add .
   git commit -m "Initial project setup"
   git push
   ```

3. **Repository operations**:
   ```bash
   # View repository information
   gh repo view
   
   # View repository in browser
   gh repo view --web
   
   # Edit repository settings
   gh repo edit --description "Updated: GitHub CLI practice repository"
   
   # List your repositories
   gh repo list
   
   # Fork someone else's repository
   gh repo fork octocat/Hello-World --clone
   ```

### Task 2: Issue Management

1. **Create issues using GitHub CLI**:
   ```bash
   # Create a bug report
   gh issue create --title "Fix login validation bug" --body "The login form doesn't validate email format properly. Steps to reproduce:
   1. Go to login page
   2. Enter invalid email
   3. Form submits without validation
   
   Expected: Show validation error
   Actual: Form submits" --label bug,priority-high
   
   # Create a feature request
   gh issue create --title "Add dark mode support" --body "Users have requested dark mode support for better usability in low-light environments." --label enhancement,feature
   
   # Create a simple issue interactively
   gh issue create
   ```

2. **Manage existing issues**:
   ```bash
   # List all issues
   gh issue list
   
   # List only open issues
   gh issue list --state open
   
   # List issues with specific labels
   gh issue list --label bug
   
   # View specific issue
   gh issue view 1
   
   # View issue in browser
   gh issue view 1 --web
   ```

3. **Issue operations**:
   ```bash
   # Comment on an issue
   gh issue comment 1 --body "I'm working on this issue and will have a fix ready soon."
   
   # Edit an issue
   gh issue edit 1 --add-label "in-progress"
   
   # Assign an issue
   gh issue edit 1 --add-assignee @me
   
   # Close an issue
   gh issue close 1 --comment "Fixed in PR #1"
   ```

### Task 3: Pull Request Workflow

1. **Create a feature branch and work on it**:
   ```bash
   git checkout -b feature/login-validation
   
   # Implement the fix
   echo "import re" > src/validation.py
   echo "" >> src/validation.py
   echo "def validate_email(email):" >> src/validation.py
   echo "    email_regex = r'^[^\\s@]+@[^\\s@]+\\.[^\\s@]+$'" >> src/validation.py
   echo "    return bool(re.match(email_regex, email))" >> src/validation.py
   
   git add src/validation.py
   git commit -m "Add email validation function"
   
   # Add tests
   echo "from src.validation import validate_email" > tests/validation_test.py
   echo "" >> tests/validation_test.py
   echo "print('Testing email validation:')" >> tests/validation_test.py
   echo "print('Valid email:', validate_email('user@example.com'))" >> tests/validation_test.py
   echo "print('Invalid email:', validate_email('invalid-email'))" >> tests/validation_test.py
   
   git add tests/validation_test.py
   git commit -m "Add validation tests"
   
   git push -u origin feature/login-validation
   ```

2. **Create pull request with GitHub CLI**:
   ```bash
   # Create PR with title and body
   gh pr create --title "Fix login validation bug" --body "This PR fixes the email validation issue reported in #1.
   
   ## Changes
   - Added validateEmail function with regex validation
   - Added comprehensive tests for validation
   - Updated login form to use validation
   
   ## Testing
   - [x] Unit tests pass
   - [x] Manual testing completed
   - [x] No console errors
   
   Fixes #1"
   
   # Alternative: Create PR interactively
   # gh pr create
   ```

3. **Pull request management**:
   ```bash
   # List all pull requests
   gh pr list
   
   # View specific PR
   gh pr view 1
   
   # Check out a PR locally for testing
   gh pr checkout 1
   
   # Review a PR
   gh pr review 1 --approve --body "LGTM! Great implementation with good test coverage."
   
   # Request changes
   gh pr review 1 --request-changes --body "Please add error handling for edge cases."
   
   # Add a comment to PR
   gh pr comment 1 --body "Thanks for the quick fix!"
   ```

4. **Merge pull request**:
   ```bash
   # Merge with different strategies
   gh pr merge 1 --squash --delete-branch
   
   # Or merge commit
   # gh pr merge 1 --merge
   
   # Or rebase
   # gh pr merge 1 --rebase
   ```

### Task 4: Advanced GitHub CLI Features

1. **Working with releases**:
   ```bash
   # Switch to main and pull latest
   git checkout main
   git pull
   
   # Create a release
   gh release create v1.0.0 --title "Version 1.0.0" --notes "First stable release with email validation feature"
   
   # Create pre-release
   gh release create v1.1.0-beta --prerelease --title "Beta Release 1.1.0" --notes "Beta release with experimental features"
   
   # List releases
   gh release list
   
   # View specific release
   gh release view v1.0.0
   ```

2. **Working with gists**:
   ```bash
   # Create a gist from a file
   echo "# Useful Python utility functions" > utils.py
   echo "import time" >> utils.py
   echo "from functools import wraps" >> utils.py
   echo "" >> utils.py
   echo "def debounce(wait):" >> utils.py
   echo "    def decorator(func):" >> utils.py
   echo "        @wraps(func)" >> utils.py
   echo "        def wrapper(*args, **kwargs):" >> utils.py
   echo "            wrapper.last_called = time.time()" >> utils.py
   echo "            def delayed():" >> utils.py
   echo "                if time.time() - wrapper.last_called >= wait:" >> utils.py
   echo "                    return func(*args, **kwargs)" >> utils.py
   echo "            return delayed()" >> utils.py
   echo "        return wrapper" >> utils.py
   echo "    return decorator" >> utils.py
   
   gh gist create utils.py --description "Python utility functions"
   
   # Create gist from multiple files
   echo "# My Code Snippets" > snippets.md
   echo "Collection of useful code snippets" >> snippets.md
   gh gist create utils.py snippets.md --description "Utility functions and documentation"
   
   # List your gists
   gh gist list
   ```

3. **GitHub Actions integration**:
   ```bash
   # Create a simple workflow
   mkdir -p .github/workflows
   cat > .github/workflows/test.yml << 'EOF'
   name: Run Tests
   on: [push, pull_request]
   jobs:
     test:
       runs-on: ubuntu-latest
       steps:
         - uses: actions/checkout@v2
         - name: Setup Python
           uses: actions/setup-python@v2
           with:
             python-version: '3.9'
         - name: Run tests
           run: python tests/validation_test.py
   EOF
   
   git add .github/workflows/test.yml
   git commit -m "Add GitHub Actions workflow"
   git push
   
   # View workflow runs
   gh run list
   
   # Watch a workflow run
   gh run watch
   
   # View specific run
   gh run view 1
   ```

### Task 5: GitHub CLI Automation and Scripting

1. **Create aliases for common operations**:
   ```bash
   # Set up useful aliases
   gh alias set prc 'pr create --fill'
   gh alias set prl 'pr list'
   gh alias set prv 'pr view'
   gh alias set prs 'pr status'
   gh alias set issues 'issue list'
   gh alias set repos 'repo list'
   
   # Test aliases
   gh prl  # Should list PRs
   gh issues  # Should list issues
   ```

2. **Create a script for common workflow**:
   ```bash
   cat > create-feature-branch.sh << 'EOF'
   #!/bin/bash
   
   # Script to create feature branch with issue
   if [ $# -eq 0 ]; then
     echo "Usage: $0 <feature-name> [issue-title]"
     exit 1
   fi
   
   FEATURE_NAME=$1
   ISSUE_TITLE=${2:-"Implement $FEATURE_NAME"}
   
   # Create issue
   ISSUE_NUMBER=$(gh issue create --title "$ISSUE_TITLE" --body "Working on $FEATURE_NAME feature" --format "%I")
   echo "Created issue #$ISSUE_NUMBER"
   
   # Create and switch to feature branch
   git checkout -b "feature/$FEATURE_NAME"
   echo "Created and switched to feature/$FEATURE_NAME branch"
   
   # Create initial commit
   echo "# $FEATURE_NAME Feature" > "$FEATURE_NAME.md"
   echo "Implementation notes for $FEATURE_NAME" >> "$FEATURE_NAME.md"
   git add "$FEATURE_NAME.md"
   git commit -m "Start work on $FEATURE_NAME (refs #$ISSUE_NUMBER)"
   
   echo "Feature branch ready! Issue: #$ISSUE_NUMBER"
   EOF
   
   chmod +x create-feature-branch.sh
   
   # Test the script
   ./create-feature-branch.sh "dark-mode" "Add dark mode support"
   ```

3. **Bulk operations script**:
   ```bash
   cat > repo-health-check.sh << 'EOF'
   #!/bin/bash
   
   echo "=== Repository Health Check ==="
   echo "Repository: $(gh repo view --json name -q .name)"
   echo "Description: $(gh repo view --json description -q .description)"
   echo ""
   
   echo "=== Issues Summary ==="
   echo "Open issues: $(gh issue list --json number | jq length)"
   echo "Closed issues: $(gh issue list --state closed --json number | jq length)"
   echo ""
   
   echo "=== Pull Requests Summary ==="
   echo "Open PRs: $(gh pr list --json number | jq length)"
   echo "Merged PRs: $(gh pr list --state merged --json number | jq length)"
   echo ""
   
   echo "=== Recent Activity ==="
   echo "Recent commits:"
   git log --oneline -5
   echo ""
   
   echo "=== Repository Stats ==="
   echo "Total files: $(git ls-files | wc -l)"
   echo "Total commits: $(git rev-list --count HEAD)"
   echo "Branches: $(git branch -r | wc -l)"
   EOF
   
   chmod +x repo-health-check.sh
   ./repo-health-check.sh
   ```

## 🎯 Advanced Challenges

### Challenge 1: Multi-Repository Management

1. **Create multiple repositories for a project ecosystem**:
   ```bash
   # Create related repositories
   gh repo create project-frontend --public --description "Frontend application"
   gh repo create project-backend --public --description "Backend API"
   gh repo create project-docs --public --description "Project documentation"
   
   # Clone all repositories
   gh repo clone project-frontend
   gh repo clone project-backend  
   gh repo clone project-docs
   ```

2. **Set up cross-repository workflow**:
   ```bash
   cd project-frontend
   echo "Frontend connecting to backend API" > integration-notes.md
   git add integration-notes.md
   git commit -m "Add backend integration notes"
   git push
   
   # Create issue linking repositories
   gh issue create --title "Integrate with backend API" --body "This frontend needs to integrate with the backend API from https://github.com/$(gh api user --jq .login)/project-backend"
   ```

### Challenge 2: GitHub CLI Extension

1. **Explore and install extensions**:
   ```bash
   # List available extensions
   gh extension list
   
   # Install a popular extension (if available)
   # gh extension install owner/gh-extension-name
   
   # Create a simple custom extension
   mkdir gh-hello
   cd gh-hello
   
   cat > gh-hello << 'EOF'
   #!/bin/bash
   echo "Hello from GitHub CLI extension!"
   echo "Current repository: $(gh repo view --json name -q .name)"
   echo "Current user: $(gh api user --jq .login)"
   EOF
   
   chmod +x gh-hello
   
   # Install locally (add to PATH)
   mkdir -p ~/.local/bin
   cp gh-hello ~/.local/bin/
   export PATH="$HOME/.local/bin:$PATH"
   
   # Test the extension
   gh hello
   ```

### Challenge 3: GitHub CLI Configuration

1. **Configure GitHub CLI for optimal workflow**:
   ```bash
   # Set preferred editor
   gh config set editor "code --wait"
   
   # Set default protocol
   gh config set git_protocol https
   
   # Set default repository for commands
   gh repo set-default
   
   # View all configuration
   gh config list
   ```

2. **Create comprehensive aliases**:
   ```bash
   # Development workflow aliases
   gh alias set start-feature 'issue create --title'
   gh alias set finish-feature 'pr create --fill'
   gh alias set review-pr 'pr review --approve'
   gh alias set ship 'pr merge --squash --delete-branch'
   
   # Information aliases  
   gh alias set my-issues 'issue list --assignee @me'
   gh alias set my-prs 'pr list --author @me'
   gh alias set repo-info 'repo view'
   gh alias set activity 'run list --limit 5'
   ```

## ✅ Verification Checklist

After completing the exercise, verify your GitHub CLI mastery:

- [ ] Can create and manage repositories with `gh repo`
- [ ] Can create, list, and manage issues with `gh issue`
- [ ] Can create, review, and merge pull requests with `gh pr`
- [ ] Can create and manage releases with `gh release`
- [ ] Can work with gists using `gh gist`
- [ ] Can monitor GitHub Actions with `gh run`
- [ ] Can create useful aliases for workflow automation
- [ ] Can write scripts that use GitHub CLI commands

## 🔍 Knowledge Check

Test your GitHub CLI understanding:

1. **What's the difference between `gh repo create` and `git init`?**
   - `gh repo create` creates repository on GitHub; `git init` creates local repository

2. **How do you link a PR to an issue using GitHub CLI?**
   - Use "Fixes #issue-number" in the PR body when creating with `gh pr create`

3. **What's the benefit of using `gh pr checkout`?**
   - Allows you to test PRs locally before merging

4. **When would you use `gh gist create`?**
   - For sharing code snippets or small files quickly

## 📊 GitHub CLI Usage Summary

Create a comprehensive summary of your GitHub CLI usage:

```bash
# Create GitHub CLI summary
echo "# GitHub CLI Mastery Summary" > gh-cli-summary.md
echo "" >> gh-cli-summary.md
echo "## Commands Mastered" >> gh-cli-summary.md
echo "- Repository management: create, clone, view, edit" >> gh-cli-summary.md
echo "- Issue management: create, list, comment, close" >> gh-cli-summary.md
echo "- Pull request workflow: create, review, merge" >> gh-cli-summary.md
echo "- Release management: create, list, view" >> gh-cli-summary.md
echo "- Gist operations: create, list" >> gh-cli-summary.md
echo "- GitHub Actions: view runs, watch workflows" >> gh-cli-summary.md
echo "" >> gh-cli-summary.md
echo "## Aliases Created" >> gh-cli-summary.md
gh alias list >> gh-cli-summary.md
echo "" >> gh-cli-summary.md
echo "## Authentication Status" >> gh-cli-summary.md
gh auth status >> gh-cli-summary.md

git add gh-cli-summary.md
git commit -m "Add GitHub CLI mastery summary"
git push
```

## 🐛 Troubleshooting Common Issues

### Issue: Authentication problems
```bash
# Re-authenticate
gh auth logout
gh auth login

# Check status
gh auth status
```

### Issue: Permission denied for repository operations
```bash
# Check if you have correct permissions
gh repo view --json permissions

# Ensure you're authenticated as the correct user
gh api user
```

### Issue: GitHub CLI commands not found
```bash
# Verify installation
gh --version

# Check PATH
which gh

# Reinstall if necessary
```

## 🎉 Congratulations!

You've mastered the GitHub CLI! You now have the power to:
- Perform all major GitHub operations from the terminal
- Automate repetitive GitHub workflows
- Create efficient development scripts
- Manage multiple repositories effectively
- Integrate GitHub operations into your daily workflow

## 🎓 Course Completion

You've completed all exercises in the Git & GitHub Fundamentals course! You now have:

✅ **Git Fundamentals**
- Installation and configuration
- Repository management
- Basic workflow (add, commit, push, pull)
- Branch management
- Merging and collaboration

✅ **GitHub Mastery**
- Pull request workflows
- Issue management
- GitHub CLI operations
- Team collaboration
- Advanced automation

**Next Steps:**
- Apply these skills to real projects
- Explore advanced Git topics (rebasing, hooks, submodules)
- Learn about Git workflows (GitFlow, GitHub Flow)
- Contribute to open source projects
- Share your knowledge with others!

Keep practicing and happy coding! 🚀
