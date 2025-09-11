# Exercise 5: Collaboration and Merging 🤝

## 🎯 Objective
Master collaborative Git workflows, including merge conflicts, pull requests, and team development practices.

## 📋 Prerequisites
- Completed Exercises 1-4
- GitHub account
- Understanding of branching and merging
- Basic knowledge of markdown

## 🚀 Exercise Tasks

### Task 1: Setting Up Collaborative Repository

1. **Create a collaborative project repository**:
   ```bash
   mkdir team-collaboration
   cd team-collaboration
   git init
   
   # Create project structure
   echo "# Team Collaboration Project" > README.md
   echo "A project to practice team Git workflows." >> README.md
   
   mkdir src docs tests
   echo "print('Main application')" > src/app.py
   echo "# Documentation" > docs/README.md
   echo "# Test file" > tests/app_test.py
   
   git add .
   git commit -m "Initial project structure"
   ```

2. **Connect to GitHub and push**:
   ```bash
   # Create repository on GitHub first, then:
   git remote add origin https://github.com/YOUR-USERNAME/team-collaboration.git
   git push -u origin main
   ```

### Task 2: Simulating Team Member A Workflow

1. **Create a feature branch for Team Member A**:
   ```bash
   git checkout -b feature/user-authentication
   ```

2. **Develop authentication feature**:
   ```bash
   # Create authentication module
   echo "class AuthService:" > src/auth.py
   echo "    def __init__(self):" >> src/auth.py
   echo "        self.users = []" >> src/auth.py
   echo "" >> src/auth.py
   echo "    def login(self, username, password):" >> src/auth.py
   echo "        print(f'Logging in: {username}')" >> src/auth.py
   echo "        return True" >> src/auth.py
   
   git add src/auth.py
   git commit -m "Add AuthService class with login method"
   ```

3. **Continue development**:
   ```bash
   echo "" >> src/auth.py
   echo "    def register(self, username, password, email):" >> src/auth.py
   echo "        print(f'Registering user: {username}')" >> src/auth.py
   echo "        self.users.append({'username': username, 'email': email})" >> src/auth.py
   echo "        return True" >> src/auth.py
   
   git add src/auth.py
   git commit -m "Add user registration functionality"
   ```

4. **Add documentation**:
   ```bash
   echo "# Authentication Module" > docs/auth.md
   echo "" >> docs/auth.md
   echo "## Usage" >> docs/auth.md
   echo "```python" >> docs/auth.md
   echo "auth = AuthService()" >> docs/auth.md
   echo "auth.login('user', 'password')" >> docs/auth.md
   echo "```" >> docs/auth.md
   
   git add docs/auth.md
   git commit -m "Add authentication documentation"
   ```

5. **Push feature branch**:
   ```bash
   git push -u origin feature/user-authentication
   ```

### Task 3: Simulating Team Member B Workflow (Different Machine)

To simulate a different team member, we'll create another directory:

1. **Clone repository as Team Member B**:
   ```bash
   cd ..
   git clone https://github.com/YOUR-USERNAME/team-collaboration.git team-member-b
   cd team-member-b
   ```

2. **Create different feature branch**:
   ```bash
   git checkout -b feature/data-validation
   ```

3. **Develop validation feature**:
   ```bash
   echo "import re" > src/validator.py
   echo "" >> src/validator.py
   echo "class Validator:" >> src/validator.py
   echo "    @staticmethod" >> src/validator.py
   echo "    def validate_email(email):" >> src/validator.py
   echo "        email_regex = r'^[^\\s@]+@[^\\s@]+\\.[^\\s@]+$'" >> src/validator.py
   echo "        return bool(re.match(email_regex, email))" >> src/validator.py
   echo "" >> src/validator.py
   echo "    @staticmethod" >> src/validator.py
   echo "    def validate_password(password):" >> src/validator.py
   echo "        return len(password) >= 8" >> src/validator.py
   
   git add src/validator.py
   git commit -m "Add email and password validation"
   ```

4. **Add tests for validation**:
   ```bash
   echo "# Validator tests" > tests/validator_test.py
   echo "from src.validator import Validator" >> tests/validator_test.py
   echo "" >> tests/validator_test.py
   echo "print('Testing email validation')" >> tests/validator_test.py
   echo "print(Validator.validate_email('test@example.com'))  # True" >> tests/validator_test.py
   echo "print(Validator.validate_email('invalid-email'))     # False" >> tests/validator_test.py
   
   git add tests/validator_test.py
   git commit -m "Add validation tests"
   ```

5. **Push Team Member B's feature**:
   ```bash
   git push -u origin feature/data-validation
   ```

### Task 4: Creating and Managing Pull Requests

If you have GitHub CLI installed:

1. **Create pull request for authentication feature**:
   ```bash
   cd ../team-collaboration  # Back to Team Member A
   git checkout feature/user-authentication
   gh pr create --title "Add User Authentication System" --body "This PR adds a complete user authentication system with login and registration functionality."
   ```

2. **Create pull request for validation feature**:
   ```bash
   cd ../team-member-b  # Team Member B
   git checkout feature/data-validation
   gh pr create --title "Add Data Validation Module" --body "This PR adds email and password validation with comprehensive tests."
   ```

3. **Review and merge PRs** (or do manually on GitHub):
   ```bash
   # List PRs
   gh pr list
   
   # Review a PR
   gh pr view 1
   
   # Merge PRs (after review)
   gh pr merge 1 --squash
   gh pr merge 2 --squash
   ```

### Task 5: Handling Merge Conflicts

1. **Create conflicting changes** (simulate both team members editing the same file):

   **Team Member A**:
   ```bash
   cd ../team-collaboration
   git checkout main
   git pull  # Get latest changes
   git checkout -b feature/app-improvements
   
   # Edit main app file
   echo "// Team Member A changes" >> src/app.js
   echo "function initializeApp() {" >> src/app.js
   echo "  console.log('App initialized by Team A');" >> src/app.js
   echo "}" >> src/app.js
   
   git add src/app.js
   git commit -m "Add app initialization by Team A"
   git push -u origin feature/app-improvements
   ```

   **Team Member B**:
   ```bash
   cd ../team-member-b
   git checkout main
   git pull
   git checkout -b feature/app-enhancements
   
   # Edit the same file differently
   echo "// Team Member B changes" >> src/app.js
   echo "function startApplication() {" >> src/app.js
   echo "  console.log('Application started by Team B');" >> src/app.js
   echo "}" >> src/app.js
   
   git add src/app.js
   git commit -m "Add app startup by Team B"
   git push -u origin feature/app-enhancements
   ```

2. **Merge first PR without conflict**:
   ```bash
   cd ../team-collaboration
   git checkout main
   git merge feature/app-improvements
   git push
   ```

3. **Try to merge second PR (will cause conflict)**:
   ```bash
   cd ../team-member-b
   git checkout main
   git pull  # Get the first merge
   git checkout feature/app-enhancements
   git merge main  # This will create a conflict
   ```

4. **Resolve the conflict**:
   ```bash
   # Open src/app.js and resolve the conflict
   # Remove conflict markers and combine both changes
   cat > src/app.js << 'EOF'
   console.log('Main application');
   // Team Member A changes
   function initializeApp() {
     console.log('App initialized by Team A');
   }
   // Team Member B changes  
   function startApplication() {
     console.log('Application started by Team B');
   }
   EOF
   
   git add src/app.js
   git commit -m "Resolve merge conflict between app initialization functions"
   git push
   ```

### Task 6: Advanced Collaboration Scenarios

1. **Rebase workflow**:
   ```bash
   cd ../team-collaboration
   git checkout main
   git pull
   git checkout -b feature/rebase-example
   
   echo "Feature using rebase" > rebase-feature.txt
   git add rebase-feature.txt
   git commit -m "Add rebase feature"
   
   # Rebase onto latest main
   git fetch origin
   git rebase origin/main
   git push -u origin feature/rebase-example
   ```

2. **Cherry-pick workflow**:
   ```bash
   # Create a hotfix that needs to be applied to multiple branches
   git checkout main
   git checkout -b hotfix/critical-bug
   
   echo "// Critical bug fix" >> src/app.js
   git add src/app.js
   git commit -m "Fix critical security bug"
   
   # Apply to main
   git checkout main
   git cherry-pick hotfix/critical-bug
   git push
   
   # Apply to other branches
   git checkout feature/rebase-example
   git cherry-pick hotfix/critical-bug
   git push
   ```

## 🎯 Advanced Team Workflow Simulation

### Task 7: Complete Team Development Cycle

1. **Sprint planning simulation**:
   ```bash
   cd ../team-collaboration
   git checkout main
   git pull
   
   # Create sprint branch
   git checkout -b sprint/v1.1
   
   # Create feature branches from sprint
   git checkout -b feature/user-profile sprint/v1.1
   git checkout -b feature/settings-page sprint/v1.1
   git checkout -b feature/notification-system sprint/v1.1
   ```

2. **Develop features in parallel**:
   ```bash
   # User profile feature
   git checkout feature/user-profile
   echo "class UserProfile {}" > src/profile.js
   git add src/profile.js
   git commit -m "Add user profile class"
   
   # Settings page feature  
   git checkout feature/settings-page
   echo "class SettingsPage {}" > src/settings.js
   git add src/settings.js
   git commit -m "Add settings page class"
   
   # Notification system
   git checkout feature/notification-system
   echo "class NotificationService {}" > src/notifications.js
   git add src/notifications.js
   git commit -m "Add notification service"
   ```

3. **Integration and testing**:
   ```bash
   # Merge features to sprint branch
   git checkout sprint/v1.1
   git merge feature/user-profile
   git merge feature/settings-page
   git merge feature/notification-system
   
   # Integration testing
   echo "// Integration tests" > tests/integration.test.js
   git add tests/integration.test.js
   git commit -m "Add integration tests for v1.1 features"
   ```

4. **Release preparation**:
   ```bash
   # Merge sprint to main
   git checkout main
   git merge sprint/v1.1
   
   # Tag the release
   git tag -a v1.1.0 -m "Release version 1.1.0"
   git push origin v1.1.0
   git push
   ```

## 🧪 Real-World Collaboration Scenarios

### Scenario 1: Code Review Process

1. **Create a feature that needs review**:
   ```bash
   git checkout -b feature/payment-integration
   
   echo "class PaymentProcessor {" > src/payment.js
   echo "  processPayment(amount, cardToken) {" >> src/payment.js
   echo "    // TODO: Add validation" >> src/payment.js
   echo "    console.log('Processing payment:', amount);" >> src/payment.js
   echo "    return { success: true, transactionId: 'tx123' };" >> src/payment.js
   echo "  }" >> src/payment.js
   echo "}" >> src/payment.js
   
   git add src/payment.js
   git commit -m "Add basic payment processing"
   git push -u origin feature/payment-integration
   ```

2. **Address review feedback**:
   ```bash
   # Simulate review feedback: "Add input validation"
   echo "class PaymentProcessor {" > src/payment.js
   echo "  processPayment(amount, cardToken) {" >> src/payment.js
   echo "    if (!amount || amount <= 0) {" >> src/payment.js
   echo "      throw new Error('Invalid amount');" >> src/payment.js
   echo "    }" >> src/payment.js
   echo "    if (!cardToken) {" >> src/payment.js
   echo "      throw new Error('Card token required');" >> src/payment.js
   echo "    }" >> src/payment.js
   echo "    console.log('Processing payment:', amount);" >> src/payment.js
   echo "    return { success: true, transactionId: 'tx123' };" >> src/payment.js
   echo "  }" >> src/payment.js
   echo "}" >> src/payment.js
   
   git add src/payment.js
   git commit -m "Add input validation based on code review feedback"
   git push
   ```

### Scenario 2: Emergency Hotfix Workflow

1. **Critical bug discovered in production**:
   ```bash
   git checkout main
   git checkout -b hotfix/auth-vulnerability
   
   # Fix the critical bug
   echo "  logout() {" >> src/auth.js
   echo "    console.log('User logged out');" >> src/auth.js
   echo "    // Clear session tokens securely" >> src/auth.js
   echo "    this.clearTokens();" >> src/auth.js
   echo "  }" >> src/auth.js
   echo "" >> src/auth.js
   echo "  clearTokens() {" >> src/auth.js
   echo "    // Secure token cleanup" >> src/auth.js
   echo "  }" >> src/auth.js
   
   git add src/auth.js
   git commit -m "Fix authentication token cleanup vulnerability"
   ```

2. **Apply hotfix to main and active branches**:
   ```bash
   # Apply to main
   git checkout main
   git merge hotfix/auth-vulnerability
   git tag -a v1.1.1 -m "Hotfix: Authentication security patch"
   git push origin v1.1.1
   git push
   
   # Apply to active feature branches
   git checkout feature/payment-integration
   git merge hotfix/auth-vulnerability
   git push
   
   # Clean up
   git branch -d hotfix/auth-vulnerability
   ```

## ✅ Verification Checklist

After completing the exercise, verify your collaboration skills:

- [ ] Can simulate multiple team members working on same repository
- [ ] Can create and manage feature branches for different team members
- [ ] Can handle merge conflicts when they occur
- [ ] Understand different merge strategies (merge vs rebase vs squash)
- [ ] Can use pull requests for code review workflow
- [ ] Can apply hotfixes to multiple branches
- [ ] Understand cherry-picking for selective change application

## 🔍 Knowledge Check

Test your understanding:

1. **When do merge conflicts occur?**
   - When the same lines in the same file are modified differently in two branches

2. **What's the difference between merge and rebase?**
   - Merge preserves history; rebase rewrites history for a linear timeline

3. **When should you use squash merge?**
   - When you want to combine all feature commits into a single commit

4. **What's cherry-picking used for?**
   - Applying specific commits from one branch to another

## 📊 Collaboration Analysis

Create a collaboration summary:

```bash
# Create collaboration analysis
echo "# Team Collaboration Exercise Summary" > collaboration-summary.md
echo "" >> collaboration-summary.md
echo "## Repository Statistics" >> collaboration-summary.md
echo "- Total commits: $(git rev-list --count HEAD)" >> collaboration-summary.md
echo "- Total branches created: [Count from exercise]" >> collaboration-summary.md
echo "- Merge conflicts resolved: [Count from exercise]" >> collaboration-summary.md
echo "- Pull requests created: [Count from exercise]" >> collaboration-summary.md
echo "" >> collaboration-summary.md
echo "## Team Members Simulated" >> collaboration-summary.md
echo "- Team Member A: Authentication & App improvements" >> collaboration-summary.md
echo "- Team Member B: Validation & App enhancements" >> collaboration-summary.md
echo "" >> collaboration-summary.md
echo "## Features Developed" >> collaboration-summary.md
git log --oneline --grep="Add\|Fix" >> collaboration-summary.md

git add collaboration-summary.md
git commit -m "Add team collaboration exercise summary"
git push
```

## 🎉 Congratulations!

You've mastered collaborative Git workflows! You now understand:
- How teams work together using Git and GitHub
- Handling merge conflicts effectively
- Different merge strategies and when to use them
- Pull request workflows for code review
- Emergency hotfix procedures
- Advanced collaboration patterns

## ➡️ Next Exercise

Ready to master the GitHub CLI? Move on to [Exercise 6: GitHub CLI Mastery](./exercise-06.md) to learn advanced GitHub operations from the command line!
