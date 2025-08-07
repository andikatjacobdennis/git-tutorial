# **Practical Git Workflow for C# Developers**  
*A complete, hands-on tutorial with real C# examples and common team scenarios*

---

## **1. Project Setup & First Commit**
### **Situation:** Starting a new C# console application for a banking system.

```bash
# Initialize project
mkdir BankApp && cd BankApp
dotnet new console
git init
git add .
git commit -m "Initial commit: Empty C# console app"
```

**Program.cs** (Initial version):
```csharp
class Program {
    static void Main() {
        Console.WriteLine("Bank App Starting...");
    }
}
```

---

## **2. Feature Development Workflow**
### **Situation:** Adding account management functionality.

### **2.1 Create Feature Branch**
```bash
git checkout -b feature/account-management
```

### **2.2 Develop Account Class**
**Account.cs**:
```csharp
public class Account {
    public int AccountId { get; }
    public decimal Balance { get; private set; }

    public Account(int accountId) {
        AccountId = accountId;
    }

    public void Deposit(decimal amount) {
        Balance += amount;
    }
}
```

```bash
git add Account.cs
git commit -m "Add basic Account class"
```

### **2.3 Add Withdrawal Method (New Commit)**
**Account.cs** (updated):
```csharp
public void Withdraw(decimal amount) {
    if (amount > Balance) 
        throw new InvalidOperationException("Insufficient funds");
    Balance -= amount;
}
```

```bash
git commit -am "Add withdrawal with validation"
```

### **2.4 Interactive Rebase Before PR**
```bash
git rebase -i HEAD~2
```
- Squash second commit into first
- Edit message: "feat: Implement Account class with deposit/withdrawal"

---

## **3. Handling Production Issues**
### **Situation:** Bug found in withdrawal logic after merge to main.

### **3.1 Create Hotfix Branch**
```bash
git checkout main
git checkout -b hotfix/withdrawal-bug
```

### **3.2 Fix the Bug**
**Account.cs** (updated):
```csharp
public void Withdraw(decimal amount) {
    if (amount <= 0)
        throw new ArgumentException("Amount must be positive");
    if (amount > Balance)
        throw new InvalidOperationException("Insufficient funds");
    Balance -= amount;
}
```

```bash
git commit -am "fix: Validate withdrawal amount"
```

### **3.3 Merge Hotfix**
```bash
git checkout main
git merge hotfix/withdrawal-bug
git push origin main
```

### **3.4 Update Feature Branch**
```bash
git checkout feature/account-management
git rebase main
```

---

## **4. Collaborative Workflow**
### **Situation:** Team member added transaction logging while you worked on accounts.

### **4.1 Fetch Changes**
```bash
git fetch origin
```

### **4.2 Rebase Your Work**
```bash
git rebase origin/main
```

### **4.3 Resolve Conflicts**
If conflicts occur in **Program.cs**:
1. Edit file to keep both features
2. Mark as resolved:
```bash
git add Program.cs
git rebase --continue
```

---

## **5. Stashing Work in Progress**
### **Situation:** Urgent bugfix needed while working on new feature.

### **5.1 Stash Current Work**
```bash
git stash push -m "WIP: Account interest calculation"
```

### **5.2 Handle Bugfix**
```bash
git checkout -b hotfix/display-issue
# Make fixes...
git commit -am "fix: Correct balance display"
git checkout main
git merge hotfix/display-issue
```

### **5.3 Restore Work**
```bash
git checkout feature/account-management
git stash pop
```

---

## **6. Undoing Mistakes**
### **Situation:** Accidentally committed sensitive data.

### **6.1 Remove Last Commit (Before Push)**
```bash
git reset --soft HEAD~1
# Remove sensitive data
git commit -m "Proper commit message"
```

### **6.2 Revert Published Commit**
```bash
git revert abc1234
git push origin main
```

### **6.3 Emergency History Rewrite**
*(Only for non-shared branches)*
```bash
git reset --hard abc1234
git push --force origin feature/x
```

---

## **7. Cherry-Picking Changes**
### **Situation:** Need to port a fix to release branch.

```bash
git checkout release/v1.0
git cherry-pick abc1234  # The bugfix commit hash
```

---

## **Complete Command Cheat Sheet**

| Scenario | Command | When to Use |
|----------|---------|-------------|
| Start new feature | `git checkout -b feature/x` | Beginning any new work |
| Save work | `git stash push -m "message"` | When interrupted |
| Share work | `git push -u origin feature/x` | Ready for review |
| Update local work | `git fetch && git rebase origin/main` | Before pushing |
| Fix mistakes | `git commit --amend` | Before pushing |
| Undo public commit | `git revert abc123` | For shared branches |
| Apply specific fix | `git cherry-pick abc123` | Porting changes |
