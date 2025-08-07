# **Git Workflow Mastery: A Hands-On Tutorial**

## **1. Repository Setup**

### **1.1 Initialize & Commit**

```bash
git init git-practice             # Initialize a new Git repository in 'git-practice' folder
cd git-practice                   # Navigate into the new project directory
echo "# Git Practice Repository" > README.md  # Create a README file with a title
git add README.md                 # Stage the README file for commit
git commit -m "Initial commit"   # Commit the file with a message
```

### **1.2 Connect to GitHub**

```bash
git remote add origin https://github.com/your-name/git-practice.git  # Link local repo to GitHub
git branch -M main              # Rename default branch to 'main'
git push -u origin main         # Push code to GitHub and set upstream
```

---

## **2. Branching & Merging**

### **2.1 Create a Feature Branch**

```bash
git checkout -b feature/login   # Create and switch to a new branch for the login feature
echo "Login Page" > login.html  # Add a placeholder login page
git add login.html              # Stage the new file
git commit -m "Add login page"  # Commit the new feature
```

### **2.2 Merge into `main`**

```bash
git checkout main               # Switch back to the main branch
git merge feature/login         # Merge changes from 'feature/login' into 'main'
git branch -d feature/login     # Delete the feature branch after merging
```

---

## **3. Rebasing**

### **3.1 Linear History with Rebase**

```bash
git checkout -b feature/dashboard         # Create a new branch for dashboard feature
echo "Dashboard UI" > dashboard.html      # Add a placeholder dashboard page
git add . && git commit -m "Add dashboard"  # Stage and commit the file
git rebase main                           # Rebase changes onto latest main (linear history)
```

### **3.2 Interactive Rebase (Squash/Rewrite Commits)**

```bash
git rebase -i HEAD~3  # Open last 3 commits for editing/squashing
```

* In the interactive editor:

  * Use `squash` to combine multiple commits into one.
  * Use `reword` to change commit messages.
  * Use `drop` to remove unwanted commits.

---

## **4. Stashing Changes**

### **4.1 Save Uncommitted Work**

```bash
echo "Unfinished code" > temp.js         # Simulate some temporary code
git stash push -m "WIP: Temp changes"    # Save current changes without committing
git stash list                           # Show list of stashed changes
```

### **4.2 Reapply Stashed Changes**

```bash
git stash pop                  # Apply latest stash and remove it from stash list
# OR
git stash apply stash@{1}     # Apply a specific stash (without removing it)
```

---

## **5. Undoing Changes**

### **5.1 Undo Last Commit (Keep Changes)**

```bash
git reset --soft HEAD~1       # Undo last commit but keep changes staged
```

### **5.2 Discard Commit & Changes**

```bash
git reset --hard HEAD~1       # ⚠️ Completely remove last commit and local changes
```

### **5.3 Revert a Commit (Safe Undo)**

```bash
git revert <commit-hash>      # Create a new commit that undoes changes from a previous one
```

### **5.4 Fix a Commit (Amend)**

```bash
git commit --amend -m "New message"  # Edit message or add files to last commit
```

---

## **6. Advanced: Cherry-Picking**

```bash
git cherry-pick <commit-hash>  # Apply a specific commit from another branch into the current one
```

---

## **7. Remote Collaboration**

### **7.1 Sync with Remote**

```bash
git fetch origin           # Fetch updates from remote (doesn't auto-merge)
git pull origin main       # Fetch and merge latest changes from remote main
```

### **7.2 Push a New Branch**

```bash
git push -u origin feature/dashboard  # Push new branch and track it with upstream
```

---

## **Best Practices for Teams**  
✔ **Branch Naming:** Use feature/, bugfix/, or hotfix/ prefixes.  
✔ **Atomic Commits:** One logical change per commit.  
✔ **Rebase Before PRs:** Keep history clean before merging.  
✔ **Stash Often:** Avoid half-baked commits.  

---

## **Quick Command Reference**

| Action             | Command                       |
| ------------------ | ----------------------------- |
| Create Branch      | `git checkout -b <name>`      |
| Merge              | `git merge <branch>`          |
| Rebase             | `git rebase main`             |
| Interactive Rebase | `git rebase -i HEAD~3`        |
| Stash Changes      | `git stash push -m "message"` |
| Undo Commit (Soft) | `git reset --soft HEAD~1`     |
| Revert Commit      | `git revert <hash>`           |
| Cherry-Pick        | `git cherry-pick <hash>`      |
