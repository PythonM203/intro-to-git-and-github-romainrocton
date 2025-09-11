# Troubleshooting Guide 🔧

## 🚨 Common Git and GitHub Issues and Solutions

This guide helps you diagnose and fix the most common Git and GitHub problems encountered during development.

## 🔐 Authentication Issues

### Issue: "Permission denied (publickey)"
**Symptoms**: Can't push to GitHub, SSH authentication fails
**Solutions**:

1. **Check SSH key setup**:
   ```bash
   # Test SSH connection
   ssh -T git@github.com
   
   # Generate new SSH key if needed
   ssh-keygen -t ed25519 -C "your.email@example.com"
   
   # Add to SSH agent
   eval "$(ssh-agent -s)"
   ssh-add ~/.ssh/id_ed25519
   
   # Copy public key to clipboard
   cat ~/.ssh/id_ed25519.pub
   ```

2. **Switch to HTTPS**:
   ```bash
   # Change remote URL to HTTPS
   git remote set-url origin https://github.com/username/repo.git
   ```

3. **Use GitHub CLI authentication**:
   ```bash
   gh auth login
   gh auth setup-git
   ```

### Issue: "Authentication failed"
**Symptoms**: GitHub CLI or Git commands fail with auth errors
**Solutions**:

```bash
# Re-authenticate GitHub CLI
gh auth logout
gh auth login

# Clear Git credentials (Windows)
git config --global --unset credential.helper
git config --global credential.helper manager-core

# Clear Git credentials (macOS)
git config --global --unset credential.helper
git config --global credential.helper osxkeychain

# Clear Git credentials (Linux)
git config --global --unset credential.helper
git config --global credential.helper store
```

## 🔄 Merge Conflicts

### Issue: Merge conflicts during pull/merge
**Symptoms**: Git stops with "CONFLICT" messages
**Solutions**:

1. **Identify conflicted files**:
   ```bash
   git status
   git diff --name-only --diff-filter=U
   ```

2. **Resolve conflicts manually**:
   ```bash
   # Open conflicted file and look for:
   # <<<<<<< HEAD
   # Your changes
   # =======
   # Their changes
   # >>>>>>> branch-name
   
   # Edit file to resolve conflicts, then:
   git add resolved-file.txt
   git commit
   ```

3. **Use merge tools**:
   ```bash
   # Configure merge tool
   git config --global merge.tool vscode
   git config --global mergetool.vscode.cmd 'code --wait $MERGED'
   
   # Use merge tool
   git mergetool
   ```

4. **Abort merge if needed**:
   ```bash
   git merge --abort
   git reset --hard HEAD
   ```

### Issue: Conflicts during rebase
**Solutions**:

```bash
# Resolve conflict, then continue
git add resolved-file.txt
git rebase --continue

# Skip this commit
git rebase --skip

# Abort rebase
git rebase --abort
```

## 🌿 Branch Issues

### Issue: "Branch not found" or wrong branch
**Solutions**:

```bash
# List all branches
git branch -a

# Fetch latest branches
git fetch --all

# Create branch from remote
git checkout -b local-branch origin/remote-branch

# Reset branch to match remote
git fetch origin
git reset --hard origin/branch-name
```

### Issue: Accidentally committed to wrong branch
**Solutions**:

```bash
# Move commits to new branch
git branch new-branch-name
git reset --hard HEAD~N  # N = number of commits to move
git checkout new-branch-name

# Or use cherry-pick
git checkout correct-branch
git cherry-pick commit-hash
git checkout wrong-branch
git reset --hard HEAD~1
```

### Issue: Can't delete branch
**Solutions**:

```bash
# Force delete local branch
git branch -D branch-name

# Delete remote branch
git push origin --delete branch-name

# Prune deleted remote branches
git remote prune origin
```

## 📝 Commit Issues

### Issue: Wrong commit message
**Solutions**:

```bash
# Fix last commit message
git commit --amend -m "Correct message"

# Fix older commit message (interactive rebase)
git rebase -i HEAD~3  # Choose how many commits back
# Change 'pick' to 'reword' for commits to fix
```

### Issue: Forgot to add files to commit
**Solutions**:

```bash
# Add files and amend last commit
git add forgotten-file.txt
git commit --amend --no-edit

# Add files and create new commit
git add forgotten-file.txt
git commit -m "Add forgotten files"
```

### Issue: Committed sensitive information
**Solutions**:

```bash
# Remove from last commit
git reset --soft HEAD~1
git reset HEAD sensitive-file.txt
echo "sensitive-file.txt" >> .gitignore
git add .gitignore
git commit -m "Add .gitignore and remove sensitive file"

# Remove from history (use carefully!)
git filter-branch --force --index-filter \
  'git rm --cached --ignore-unmatch sensitive-file.txt' \
  --prune-empty --tag-name-filter cat -- --all
```

## 🔄 Push/Pull Issues

### Issue: "Push rejected" or "Non-fast-forward"
**Solutions**:

```bash
# Pull and merge
git pull origin main

# Pull with rebase
git pull --rebase origin main

# Force push (use carefully!)
git push --force-with-lease origin branch-name
```

### Issue: "Repository not found"
**Solutions**:

```bash
# Check remote URL
git remote -v

# Fix remote URL
git remote set-url origin https://github.com/correct-user/correct-repo.git

# Check repository access
gh repo view owner/repo
```

### Issue: Large file push rejected
**Solutions**:

```bash
# Remove large file from history
git filter-branch --force --index-filter \
  'git rm --cached --ignore-unmatch large-file.zip' \
  --prune-empty --tag-name-filter cat -- --all

# Use Git LFS for large files
git lfs install
git lfs track "*.zip"
git add .gitattributes
git add large-file.zip
git commit -m "Add large file with LFS"
```

## 🗂️ File and Directory Issues

### Issue: Untracked files showing up
**Solutions**:

```bash
# Add to .gitignore
echo "unwanted-file.txt" >> .gitignore
echo "unwanted-directory/" >> .gitignore
git add .gitignore
git commit -m "Update .gitignore"

# Remove already tracked file
git rm --cached unwanted-file.txt
echo "unwanted-file.txt" >> .gitignore
git add .gitignore
git commit -m "Remove and ignore unwanted file"
```

### Issue: File permissions changed
**Solutions**:

```bash
# Ignore file permission changes
git config core.fileMode false

# Reset file permissions
git diff --summary | grep --color=never "mode change" | cut -d' ' -f7- | xargs git checkout HEAD --
```

### Issue: Case sensitivity problems
**Solutions**:

```bash
# Rename file with case change
git mv filename.txt temp-filename.txt
git mv temp-filename.txt Filename.txt

# Configure case sensitivity
git config core.ignorecase false
```

## 🏷️ Tag Issues

### Issue: Wrong tag or need to move tag
**Solutions**:

```bash
# Delete tag locally and remotely
git tag -d v1.0.0
git push origin --delete v1.0.0

# Create new tag
git tag -a v1.0.0 -m "Version 1.0.0" commit-hash
git push origin v1.0.0

# Move tag to different commit
git tag -f v1.0.0 new-commit-hash
git push origin v1.0.0 --force
```

## 🔧 Repository Corruption

### Issue: "Object file is corrupt"
**Solutions**:

```bash
# Check repository integrity
git fsck --full

# Recover from corruption
git reflog expire --expire=now --all
git gc --prune=now --aggressive

# Clone fresh copy if corruption is severe
cd ..
git clone https://github.com/user/repo.git repo-fresh
cd repo-fresh
```

### Issue: ".git directory missing or corrupted"
**Solutions**:

```bash
# Re-initialize Git (loses history)
git init
git remote add origin https://github.com/user/repo.git
git fetch
git reset --hard origin/main

# Or clone fresh copy
rm -rf .git
git clone https://github.com/user/repo.git .
```

## 🌐 GitHub-Specific Issues

### Issue: GitHub CLI not working
**Solutions**:

```bash
# Check version and update
gh --version
gh extension upgrade --all

# Re-authenticate
gh auth logout
gh auth login

# Check GitHub status
curl -s https://www.githubstatus.com/api/v2/status.json
```

### Issue: Pull request conflicts
**Solutions**:

```bash
# Update branch with latest main
git checkout feature-branch
git fetch origin
git merge origin/main

# Resolve conflicts and push
git add .
git commit -m "Resolve merge conflicts"
git push
```

### Issue: Repository access denied
**Solutions**:

```bash
# Check permissions
gh api repos/owner/repo --jq .permissions

# Verify you're logged in as correct user
gh api user --jq .login

# Check if repository exists
gh repo view owner/repo
```

## 💻 Environment Issues

### Issue: Git not found or wrong version
**Solutions**:

```bash
# Check Git installation
which git
git --version

# Update Git (macOS with Homebrew)
brew upgrade git

# Update Git (Windows with winget)
winget upgrade Git.Git

# Update Git (Linux)
sudo apt update && sudo apt upgrade git
```

### Issue: Line ending problems
**Solutions**:

```bash
# Configure line endings globally
# Windows
git config --global core.autocrlf true

# macOS/Linux
git config --global core.autocrlf input

# Fix existing repository
git add . -u
git commit -m "Normalize line endings"
```

### Issue: Editor not opening
**Solutions**:

```bash
# Set default editor
git config --global core.editor "code --wait"
git config --global core.editor "nano"
git config --global core.editor "vim"

# Test editor
git config --global --edit
```

## 🚑 Emergency Recovery

### Issue: Lost commits after reset
**Solutions**:

```bash
# Use reflog to find lost commits
git reflog

# Recover lost commit
git checkout -b recovery commit-hash
git cherry-pick commit-hash
```

### Issue: Accidentally deleted repository
**Solutions**:

```bash
# Check GitHub for repository
gh repo view owner/repo

# Clone from GitHub if available
git clone https://github.com/owner/repo.git

# Check local backups
find ~ -name ".git" -type d 2>/dev/null | grep repo-name
```

### Issue: Need to undo everything
**Solutions**:

```bash
# Reset to specific commit (loses changes)
git reset --hard commit-hash

# Reset to last known good state
git reset --hard origin/main

# Start over completely
rm -rf .git
git init
git remote add origin https://github.com/user/repo.git
git fetch
git reset --hard origin/main
```

## 🔍 Diagnostic Commands

### Check Repository Health
```bash
# Overall status
git status

# Check for corruption
git fsck --full

# Check configuration
git config --list

# Check remotes
git remote -v

# Check branches
git branch -a

# Check recent activity
git reflog --oneline -10
```

### Debug Information
```bash
# Verbose output
GIT_TRACE=1 git command
GIT_CURL_VERBOSE=1 git push

# Check GitHub connectivity
curl -I https://api.github.com

# Check SSH connectivity
ssh -T git@github.com -v
```

## 📞 Getting Help

### Built-in Help
```bash
# General help
git help
gh help

# Command-specific help
git help command-name
gh help command-name

# Quick help
git command-name -h
gh command-name -h
```

### Online Resources
- [Git Documentation](https://git-scm.com/doc)
- [GitHub Docs](https://docs.github.com)
- [GitHub Community](https://github.community)
- [Stack Overflow Git Tag](https://stackoverflow.com/questions/tagged/git)

### When All Else Fails
1. **Create a backup** of your current work
2. **Document the exact error** messages
3. **Search for the specific error** online
4. **Ask for help** with detailed information about:
   - What you were trying to do
   - What commands you ran
   - What error messages you received
   - Your environment (OS, Git version, etc.)

---

**💡 Pro Tip**: Always create backups before attempting major recovery operations!
