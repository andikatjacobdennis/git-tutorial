# **Git Tutorial**

## **Learning Objectives**

By the end of this module, students will be able to:

  - Initialize and manage Git repositories
  - Implement branching strategies and merge workflows
  - Utilize advanced Git features like rebasing and cherry-picking
  - Collaborate effectively using remote repositories
  - Apply Git best practices in team environments

-----

## **1. Repository Setup**

*Duration: 45 minutes*

### **1.1 Initialize & Commit**

```bash
git init git-practice               # Initializes a new Git repository named 'git-practice'
cd git-practice                     # Changes the current directory to the newly created 'git-practice' folder
echo "# Git Practice" > README.md   # Creates a new file named 'README.md' and writes the heading into it
git add README.md                   # Stages the 'README.md' file, preparing it to be included in the next commit
git commit -m "Initial commit"      # Commits the staged changes to the repository with a descriptive message
```

### **1.2 Connect to GitHub**

```bash
git remote add origin [repo-url]    # Links the local repository to a remote repository on a service like GitHub, naming the remote 'origin'
git branch -M main                  # Renames the current branch (commonly 'master') to 'main'
git push -u origin main             # Pushes the 'main' branch and its commits to the 'origin' remote repository for the first time, setting 'origin/main' as the upstream branch
```

**Key Concepts:**

  - Version Control System basics
  - Local vs remote repositories
  - Git staging area

**Quiz 1: Repository Basics**

1.  What command initializes a new Git repository?
    a) `git start`
    b) `git init` ✓
    c) `git new`
    d) `git create`

2.  What does `git add` do?
    a) Commits changes
    b) Stages changes ✓
    c) Creates new branch
    d) Pushes to remote

3.  True/False: `git commit -m` saves changes locally without a message.
    a) True
    b) False ✓ (The `-m` flag requires a message)

-----

## **2. Branching & Merging**

*Duration: 60 minutes*

### **2.1 Feature Branch Workflow**

```bash
git checkout -b feature/login       # Creates a new branch named 'feature/login' and immediately switches to it
echo "content" > login.html         # Creates a new file named 'login.html' with "content" inside
git add . && git commit -m "Add login" # Stages all new and modified files in the current directory and commits them with a message
```

### **2.2 Merge Process**

```bash
git checkout main                   # Switches back to the 'main' branch
git merge feature/login             # Merges the changes from the 'feature/login' branch into the current 'main' branch
git branch -d feature/login         # Deletes the 'feature/login' branch after it has been successfully merged
```

**Key Concepts:**

  - Branch isolation
  - Merge strategies
  - Conflict resolution

**Quiz 2: Branching**

1.  What command creates and switches to a new branch?
    a) `git branch`
    b) `git checkout -b` ✓
    c) `git new branch`
    d) `git create branch`

2.  What's the safest merge strategy for teams?
    a) Fast-forward
    b) Squash merge
    c) Three-way merge ✓
    d) Rebase merge

3.  How do you delete a merged branch?
    a) `git remove branch`
    b) `git branch -d` ✓
    c) `git delete branch`
    d) `git branch --delete`

-----

## **3. Rebasing**

*Duration: 45 minutes*

### **3.1 Linear History**

```bash
git rebase main                     # Replays the commits from the current branch on top of the 'main' branch, creating a linear history
```

### **3.2 Interactive Rebase**

```bash
git rebase -i HEAD~3                # Starts an interactive rebase session for the last 3 commits on the current branch, allowing for editing, reordering, or squashing commits
```

**Quiz 3: Rebasing**

1.  What's the main advantage of rebasing?
    a) Creates merge commits
    b) Maintains linear history ✓
    c) Easier conflict resolution
    d) Better for remote branches

2.  Which command starts interactive rebase?
    a) `git rebase --interactive`
    b) `git rebase -i` ✓
    c) `git interactive rebase`
    d) `git rebase --edit`

-----

## **4. Stashing Changes**

*Duration: 30 minutes*

```bash
git stash push -m "WIP"             # Temporarily saves (stashes) uncommitted changes with a descriptive message "WIP" (Work In Progress)
git stash list                      # Displays a list of all stashed changes
git stash pop                       # Applies the most recently stashed changes and then deletes them from the stash list
```

**Quiz 4: Stashing**

1.  How do you view stashed changes?
    a) `git stash show`
    b) `git stash list` ✓
    c) `git stash view`
    d) `git stash --all`

-----

## **5. Undoing Changes**

*Duration: 45 minutes*

```bash
git reset --soft HEAD~1             # Undoes the last commit but keeps the changes staged in the index
git revert <hash>                   # Creates a new commit that undoes the changes introduced in a specific commit, identified by its hash
git commit --amend                  # Modifies the most recent commit by adding any newly staged changes and allowing for a new commit message
```

**Quiz 5: Undoing Changes**

1.  What's the difference between reset and revert?
    (Short answer question)
      * `git reset` moves the branch pointer, effectively erasing commit history (locally). `git revert` creates a new commit that undoes changes, preserving the commit history.

-----

## **6. Advanced Operations**

*Duration: 60 minutes*

### **6.1 Cherry-Picking**

```bash
git cherry-pick <commit-hash>       # Applies a single, specific commit from another branch to the current branch
```

### **6.2 Tagging**

```bash
git tag -a v1.0 -m "Release version" # Creates an annotated tag named 'v1.0' on the current commit, with a message describing the tag
```

-----

## **7. Team Collaboration**

*Duration: 60 minutes*

### **7.1 Pull Requests**

```bash
git push origin feature-branch      # Pushes the 'feature-branch' to the remote repository, making it available for a pull request
# Create PR via GitHub UI           # Instructs the user to navigate to the GitHub website to create a pull request (PR)
```

### **7.2 Code Reviews**

  - PR templates
  - Review guidelines
  - Approval workflows

-----

## **Assessment**

*Graded Lab Exercise*

1.  **Initialize repository (10pts)**

      - Start a new Git project.
      - Create a file and add some content.
      - Commit these changes with a message.

2.  **Implement feature branch workflow (20pts)**

      - Create a new branch for a feature.
      - Add new files or content within this feature branch.
      - Commit the changes on the new branch.
      - Switch back to the main branch.
      - Merge the feature branch's changes into the main branch.
      - Delete the feature branch.

3.  **Resolve a merge conflict (30pts)**

      - Create a situation where two branches modify the same line of a file.
      - Merge the branches, which will cause a conflict.
      - Open the file and manually edit it to resolve the conflicting lines.
      - Stage and commit the corrected file to finalize the merge.

4.  **Demonstrate rebase (20pts)**

      - Create a branch and make a commit.
      - Go back to the main branch and make a new commit.
      - Switch back to your feature branch and rebase it onto the main branch to create a linear history.

5.  **Team collaboration task (20pts)**

      - Push a local branch to a remote repository (e.g., GitHub).
      - Create a pull request (PR) from this branch to the main branch using the remote repository's interface.
      - After the PR is merged, pull the changes back into your local main branch.

**Passing Grade: 70/100**
