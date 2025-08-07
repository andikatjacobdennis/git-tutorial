## **1. Repository Setup**

### **1.1 Initialize & Commit**

```bash
git init git-practice
cd git-practice
echo "# Git Practice" > README.md
git add README.md
git commit -m "Initial commit"
```

### **1.2 Connect to GitHub**

```bash
git remote add origin [repo-url]
git branch -M main
git push -u origin main
```

---

## **2. Branching & Merging**

### **2.1 Feature Branch Workflow**

```bash
git checkout -b feature/login
echo "content" > login.html
git add . && git commit -m "Add login"
```

### **2.2 Merge Process**

```bash
git checkout main
git merge feature/login
git branch -d feature/login
```

---

## **3. Rebasing**

### **3.1 Linear History**

```bash
git rebase main
```

### **3.2 Interactive Rebase**

```bash
git rebase -i HEAD~3
```

---

## **4. Stashing Changes**

```bash
git stash push -m "WIP"
git stash list
git stash pop
```

---

## **5. Undoing Changes**

```bash
git reset --soft HEAD~1
git revert <hash>
git commit --amend
```

---

## **6. Advanced Operations**

### **6.1 Cherry-Picking**

```bash
git cherry-pick <commit-hash>
```

### **6.2 Tagging**

```bash
git tag -a v1.0 -m "Release version"
```

---

## **7. Team Collaboration**

### **7.1 Pull Requests**

```bash
git push origin feature-branch
# Create PR via GitHub UI
```

