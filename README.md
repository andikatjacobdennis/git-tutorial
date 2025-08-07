# **Git Workflow Mastery: A Hands-On Tutorial**  

## **1. Repository Setup**  
### **1.1 Initialize & Commit**  
```bash
git init git-practice
cd git-practice
echo "# Git Practice Repository" > README.md
git add README.md
git commit -m "Initial commit"
```

### **1.2 Connect to GitHub**  
```bash
git remote add origin https://github.com/andikatjacobdennis/git-practice.git
git branch -M main
git push -u origin main
```

---

## **2. Branching & Merging**  
### **2.1 Create a Feature Branch**  
```bash
git checkout -b feature/login
echo "Login Page" > login.html
git add login.html
git commit -m "Add login page"
```

### **2.2 Merge into `main`**  
```bash
git checkout main
git merge feature/login  # Fast-forward merge
git branch -d feature/login  # Delete branch
```

---

## **3. Rebasing**  
### **3.1 Linear History with Rebase**  
```bash
git checkout -b feature/dashboard
echo "Dashboard UI" > dashboard.html
git add . && git commit -m "Add dashboard"
git rebase main  # Rebase onto main
```

### **3.2 Interactive Rebase (Squash/Rewrite Commits)**  
```bash
git rebase -i HEAD~3  # Combine last 3 commits
```
- In the interactive editor:  
  - Use `squash` to merge commits.  
  - Use `reword` to edit messages.  
  - Use `drop` to remove commits.  

---

## **4. Stashing Changes**  
### **4.1 Save Uncommitted Work**  
```bash
echo "Unfinished code" > temp.js
git stash push -m "WIP: Temp changes"  # Stash changes
git stash list  # View stashes
```

### **4.2 Reapply Stashed Changes**  
```bash
git stash pop  # Apply and remove the latest stash
# OR
git stash apply stash@{1}  # Apply a specific stash
```

---

## **5. Undoing Changes**  
### **5.1 Undo Last Commit (Keep Changes)**  
```bash
git reset --soft HEAD~1  # Keeps changes staged
```

### **5.2 Discard Commit & Changes**  
```bash
git reset --hard HEAD~1  # ⚠️ Deletes commit and changes
```

### **5.3 Revert a Commit (Safe Undo)**  
```bash
git revert <commit-hash>  # Creates a new undo commit
```

### **5.4 Fix a Commit (Amend)**  
```bash
git commit --amend -m "New message"  # Edit last commit
```

---

## **6. Advanced: Cherry-Picking**  
```bash
git cherry-pick <commit-hash>  # Copy a commit from another branch
```

---

## **7. Remote Collaboration**  
### **7.1 Sync with Remote**  
```bash
git fetch origin  # Check for remote changes
git pull origin main  # Pull updates
```

### **7.2 Push a New Branch**  
```bash
git push -u origin feature/dashboard
```

---

## **Best Practices for Teams**  
✔ **Branch Naming:** Use `feature/`, `bugfix/`, or `hotfix/` prefixes.  
✔ **Atomic Commits:** One logical change per commit.  
✔ **Rebase Before PRs:** Keep history clean before merging.  
✔ **Stash Often:** Avoid half-baked commits.  

---

## **Quick Command Reference**  
| Action                | Command                          |
|-----------------------|----------------------------------|
| Create Branch         | `git checkout -b <name>`         |
| Merge                 | `git merge <branch>`             |
| Rebase                | `git rebase main`                |
| Interactive Rebase    | `git rebase -i HEAD~3`           |
| Stash Changes         | `git stash push -m "message"`    |
| Undo Commit (Soft)    | `git reset --soft HEAD~1`        |
| Revert Commit         | `git revert <hash>`              |
| Cherry-Pick           | `git cherry-pick <hash>`         |
