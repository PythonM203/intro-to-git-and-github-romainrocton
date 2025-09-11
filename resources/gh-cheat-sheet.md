# GitHub CLI Cheat Sheet 🚀

## 📋 Quick Reference for GitHub CLI (gh) Commands

Essential GitHub CLI commands for efficient GitHub operations from the terminal.

## 🔐 Authentication

```bash
# Login to GitHub
gh auth login

# Check authentication status
gh auth status

# List authenticated accounts
gh auth list

# Switch between accounts
gh auth switch

# Logout
gh auth logout

# Setup Git with GitHub credentials
gh auth setup-git
```

## 📁 Repository Management

### Creating Repositories
```bash
# Create public repository
gh repo create my-repo --public

# Create private repository
gh repo create my-repo --private

# Create with description
gh repo create my-repo --description "My awesome project"

# Create and clone
gh repo create my-repo --public --clone

# Create from current directory
gh repo create --source=. --public --push
```

### Repository Operations
```bash
# Clone repository
gh repo clone owner/repo-name

# Fork repository
gh repo fork owner/repo-name

# Fork and clone
gh repo fork owner/repo-name --clone

# View repository
gh repo view
gh repo view owner/repo-name

# View in browser
gh repo view --web

# List repositories
gh repo list
gh repo list owner-name
gh repo list --limit 20

# Edit repository
gh repo edit --description "New description"
gh repo edit --visibility private

# Delete repository
gh repo delete owner/repo-name
```

## 🐛 Issue Management

### Creating Issues
```bash
# Create issue interactively
gh issue create

# Create with title and body
gh issue create --title "Bug report" --body "Description of the bug"

# Create with labels
gh issue create --title "Feature request" --label enhancement,feature

# Create with assignees
gh issue create --title "Bug fix" --assignee username1,username2

# Create from template
gh issue create --template bug_report.md
```

### Managing Issues
```bash
# List issues
gh issue list

# List with filters
gh issue list --state open
gh issue list --state closed
gh issue list --label bug
gh issue list --assignee username
gh issue list --author username

# View issue
gh issue view 123
gh issue view 123 --web

# Edit issue
gh issue edit 123 --title "New title"
gh issue edit 123 --body "New description"
gh issue edit 123 --add-label urgent
gh issue edit 123 --remove-label wontfix
gh issue edit 123 --add-assignee username

# Close/reopen issue
gh issue close 123
gh issue close 123 --comment "Fixed in PR #456"
gh issue reopen 123

# Comment on issue
gh issue comment 123 --body "This is a comment"
```

## 🔄 Pull Request Management

### Creating Pull Requests
```bash
# Create PR interactively
gh pr create

# Create with title and body
gh pr create --title "Add new feature" --body "Description of changes"

# Create filling from commits
gh pr create --fill

# Create draft PR
gh pr create --draft

# Create to specific branch
gh pr create --base develop

# Create with reviewers and assignees
gh pr create --reviewer user1,user2 --assignee user3

# Create with labels
gh pr create --label bug,priority-high
```

### Managing Pull Requests
```bash
# List pull requests
gh pr list

# List with filters
gh pr list --state open
gh pr list --state merged
gh pr list --author username
gh pr list --assignee username
gh pr list --label bug

# View PR
gh pr view 123
gh pr view 123 --web

# Check out PR locally
gh pr checkout 123

# Edit PR
gh pr edit 123 --title "New title"
gh pr edit 123 --body "New description"
gh pr edit 123 --add-reviewer username

# View PR status
gh pr status

# View PR diff
gh pr diff 123
```

### Reviewing Pull Requests
```bash
# Review PR
gh pr review 123

# Approve PR
gh pr review 123 --approve

# Request changes
gh pr review 123 --request-changes --body "Please fix formatting"

# Comment on PR
gh pr review 123 --comment --body "Looks good overall"

# Add single comment
gh pr comment 123 --body "Great work!"
```

### Merging Pull Requests
```bash
# Merge PR (merge commit)
gh pr merge 123 --merge

# Squash and merge
gh pr merge 123 --squash

# Rebase and merge
gh pr merge 123 --rebase

# Auto-merge when checks pass
gh pr merge 123 --auto --squash

# Merge and delete branch
gh pr merge 123 --squash --delete-branch

# Close PR without merging
gh pr close 123
```

## 🏷️ Release Management

```bash
# Create release
gh release create v1.0.0

# Create with notes
gh release create v1.0.0 --notes "Release notes here"

# Create with auto-generated notes
gh release create v1.0.0 --generate-notes

# Create pre-release
gh release create v1.0.0-beta --prerelease

# Create with assets
gh release create v1.0.0 ./dist/*.zip

# List releases
gh release list

# View release
gh release view v1.0.0
gh release view v1.0.0 --web

# Download release assets
gh release download v1.0.0

# Delete release
gh release delete v1.0.0
```

## 📄 Gist Management

```bash
# Create gist from file
gh gist create file.txt

# Create gist from stdin
echo "Hello World" | gh gist create

# Create with description
gh gist create file.txt --description "Useful script"

# Create public gist
gh gist create file.txt --public

# List gists
gh gist list

# View gist
gh gist view gist-id

# Edit gist
gh gist edit gist-id

# Clone gist
gh gist clone gist-id
```

## ⚙️ GitHub Actions

```bash
# List workflow runs
gh run list

# List for specific workflow
gh run list --workflow=ci.yml

# View run details
gh run view 123456789

# Watch run in real-time
gh run watch 123456789

# Re-run workflow
gh run rerun 123456789

# Cancel run
gh run cancel 123456789

# Download artifacts
gh run download 123456789

# View workflow logs
gh run view 123456789 --log
```

## 👥 Organization and Team Management

```bash
# List organizations
gh org list

# List organization members
gh org list-members organization-name

# List teams
gh team list --org organization-name

# View team members
gh team view organization-name/team-name
```

## 🔧 Configuration and Aliases

### Configuration
```bash
# Set editor
gh config set editor "code --wait"

# Set Git protocol
gh config set git_protocol https

# View configuration
gh config list

# Set default repository
gh repo set-default owner/repo
```

### Aliases
```bash
# Create aliases
gh alias set prc 'pr create'
gh alias set prl 'pr list'
gh alias set prv 'pr view'
gh alias set prs 'pr status'
gh alias set co 'pr checkout'

# List aliases
gh alias list

# Delete alias
gh alias delete prc

# Example workflow aliases
gh alias set issues 'issue list --assignee @me'
gh alias set my-prs 'pr list --author @me'
gh alias set review 'pr review --approve'
gh alias set ship 'pr merge --squash --delete-branch'
```

## 🔍 Search and Discovery

```bash
# Search repositories
gh search repos "machine learning" --language python

# Search issues
gh search issues "bug" --repo owner/repo

# Search pull requests
gh search prs "feature" --state open

# Search code
gh search code "function myFunction"

# Search users
gh search users "location:Seattle"
```

## 📊 API Access

```bash
# Make API calls
gh api user
gh api repos/owner/repo
gh api repos/owner/repo/issues

# Get specific fields
gh api user --jq .login
gh api repos/owner/repo --jq .stargazers_count

# POST requests
gh api repos/owner/repo/issues -f title="New issue" -f body="Issue description"
```

## 🎯 Workflow Examples

### Daily Development Flow
```bash
# Morning routine
gh pr list --author @me
gh issue list --assignee @me
gh run list --limit 5

# Start new feature
gh issue create --title "Add dark mode"
git checkout -b feature/dark-mode
# ... make changes ...
git push -u origin feature/dark-mode
gh pr create --fill

# Review others' work
gh pr list
gh pr checkout 123
# ... test changes ...
gh pr review 123 --approve

# Merge your PR
gh pr merge 456 --squash --delete-branch
```

### Release Process
```bash
# Prepare release
gh pr list --base main --state open
gh run list --workflow=ci.yml

# Create release
git tag v1.2.0
git push --tags
gh release create v1.2.0 --generate-notes

# Post-release
gh issue list --milestone v1.2.0
```

### Bug Fix Workflow
```bash
# Report bug
gh issue create --title "Login fails on mobile" --label bug,mobile

# Quick fix
git checkout -b hotfix/mobile-login
# ... fix the bug ...
git push -u origin hotfix/mobile-login
gh pr create --title "Fix mobile login issue" --body "Fixes #123"

# Fast-track review and merge
gh pr merge --squash --delete-branch
gh issue close 123 --comment "Fixed in latest release"
```

## 📱 Extensions

```bash
# List available extensions
gh extension list

# Install extension
gh extension install owner/gh-extension-name

# Upgrade extensions
gh extension upgrade --all

# Remove extension
gh extension remove extension-name

# Popular extensions
gh extension install github/gh-copilot
gh extension install dlvhdr/gh-dash
gh extension install vilmibm/gh-screensaver
```

## 🚨 Troubleshooting

### Common Issues
```bash
# Authentication problems
gh auth status
gh auth logout && gh auth login

# Permission issues
gh api user  # Check if authenticated correctly
gh repo view --json permissions

# Rate limiting
gh api rate_limit

# Clear cached credentials
gh auth logout
rm -rf ~/.config/gh
gh auth login
```

### Debugging Commands
```bash
# Verbose output
gh --debug command

# Check version
gh --version

# Get help
gh help
gh help command-name
```

## 💡 Pro Tips

### Productivity Hacks
```bash
# Open current repo in browser
gh repo view --web

# Quick PR creation
gh pr create --fill  # Uses commit messages

# Auto-approve your own PRs (use carefully)
gh alias set approve-mine 'pr review --approve $(gh pr view --json number -q .number)'

# Bulk operations
for pr in $(gh pr list --json number -q '.[].number'); do
  gh pr review $pr --approve
done
```

### Integration with Git
```bash
# After git push
gh pr create --fill

# During code review
git checkout main
gh pr checkout 123  # Test the PR
gh pr review 123 --approve

# Release workflow
git tag v1.0.0
git push --tags
gh release create v1.0.0 --generate-notes
```

---

**💡 Pro Tip**: Use `gh alias` to create shortcuts for your most common workflows!
