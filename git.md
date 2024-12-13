Here’s a **comprehensive Git cheat sheet** to help you master version control quickly and effectively!

---

# **Git Cheat Sheet**

Git is a **distributed version control system** that tracks changes to files and facilitates collaboration among developers.

---

## **1. Setup and Configuration**

### **Install Git**
- Download and install Git: [https://git-scm.com](https://git-scm.com)

### **Check Git Version**
```bash
git --version
```

### **Configure Git**
Set your identity and preferences:
```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

Check current configuration:
```bash
git config --list
```

---

## **2. Basic Commands**

### **Initialize a Repository**
Create a new Git repository in a folder:
```bash
git init
```

### **Clone an Existing Repository**
Copy a remote repository to your local machine:
```bash
git clone <repo-url>
```

---

## **3. Working with Files**

### **Check Repository Status**
Show untracked, staged, and modified files:
```bash
git status
```

### **Stage Files (Add to Staging Area)**
Add a single file:
```bash
git add <filename>
```

Add all files:
```bash
git add .
```

### **Commit Changes**
Record changes to the repository:
```bash
git commit -m "Your commit message"
```

Stage and commit simultaneously:
```bash
git commit -a -m "Your commit message"
```

### **Remove Files**
Remove files from Git tracking:
```bash
git rm <filename>
```

---

## **4. Viewing Changes**

### **Show Differences**
- Compare working directory and staging area:
```bash
git diff
```

- Compare staging area and last commit:
```bash
git diff --cached
```

### **View Commit History**
See a list of commits:
```bash
git log
```

Shorter log summary:
```bash
git log --oneline
```

---

## **5. Branching**

### **List Branches**
List all branches:
```bash
git branch
```

### **Create a New Branch**
```bash
git branch <branch-name>
```

### **Switch to a Branch**
```bash
git checkout <branch-name>
```

Or create and switch to a branch in one step:
```bash
git checkout -b <branch-name>
```

### **Merge Branches**
Merge a branch into the current branch:
```bash
git merge <branch-name>
```

### **Delete a Branch**
Delete a local branch:
```bash
git branch -d <branch-name>
```

Force delete:
```bash
git branch -D <branch-name>
```

---

## **6. Remote Repositories**

### **View Remote Repositories**
List all remotes:
```bash
git remote -v
```

### **Add a Remote**
```bash
git remote add <name> <repo-url>
```

### **Fetch and Pull Changes**
- **Fetch**: Download changes without applying them:
```bash
git fetch
```

- **Pull**: Fetch and merge changes:
```bash
git pull
```

### **Push Changes**
Push local changes to a remote repository:
```bash
git push origin <branch-name>
```

---

## **7. Stashing Changes**

### **Stash Uncommitted Changes**
Save changes for later:
```bash
git stash
```

### **View Stashes**
List all stashes:
```bash
git stash list
```

### **Apply Stashed Changes**
Apply the most recent stash:
```bash
git stash apply
```

Apply and remove the stash:
```bash
git stash pop
```

---

## **8. Undoing Changes**

### **Unstage Files**
Remove from staging area but keep changes:
```bash
git reset <file>
```

Unstage everything:
```bash
git reset
```

### **Discard Changes**
Revert changes in a file:
```bash
git checkout -- <file>
```

Discard all changes in the working directory:
```bash
git reset --hard
```

### **Revert Commits**
Create a new commit that undoes a previous commit:
```bash
git revert <commit-hash>
```

---

## **9. Tags**

### **List Tags**
```bash
git tag
```

### **Create a Tag**
Create an annotated tag:
```bash
git tag -a <tag-name> -m "Tag message"
```

Create a lightweight tag:
```bash
git tag <tag-name>
```

### **Push Tags**
Push all tags to the remote repository:
```bash
git push --tags
```

---

## **10. Git Ignore**

### **Create a `.gitignore` File**
Specify files and directories to ignore:
```plaintext
# Example .gitignore
*.log
__pycache__/
node_modules/
.env
```

Apply `.gitignore` changes:
```bash
git rm --cached <file>
```

---

## **11. Rebasing**

### **Rebase a Branch**
Reapply commits from one branch onto another:
```bash
git rebase <base-branch>
```

### **Interactive Rebase**
Modify, squash, or drop commits:
```bash
git rebase -i <commit-hash>
```

---

## **12. Resolving Merge Conflicts**

### **Identify Conflicts**
During a merge or rebase, Git will mark conflicts:
```bash
git status
```

### **Resolve and Commit**
1. Edit conflicting files manually.  
2. Add resolved files:
```bash
git add <file>
```
3. Complete the merge:
```bash
git commit
```

---

## **13. Useful Shortcuts**

### **Alias Common Commands**
Simplify Git commands with aliases:
```bash
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
```

Use your aliases:
```bash
git co <branch-name>
git st
```

---

## **14. Inspect and Clean Up**

### **Check Disk Usage**
```bash
git gc
```

### **Remove Untracked Files**
Clean untracked files and directories:
```bash
git clean -f -d
```

---

## **15. Git Workflow Strategies**

### **Feature Branch Workflow**
1. Create a feature branch:  
   ```bash
   git checkout -b feature/<feature-name>
   ```

2. Develop and commit changes.  

3. Merge into `main`/`master`:  
   ```bash
   git checkout main
   git merge feature/<feature-name>
   ```

### **Git Flow**
Structured workflow with feature, release, hotfix, and bugfix branches.

- **Main Branch**: Stable production code  
- **Develop Branch**: Integration branch  
- **Feature Branch**: New features  
- **Hotfix Branch**: Urgent fixes  

---

## **16. Git and GitHub**

### **Forking a Repository**
1. Fork the repository on GitHub.  
2. Clone your fork:  
   ```bash
   git clone <your-fork-url>
   ```

3. Add upstream repository:  
   ```bash
   git remote add upstream <original-repo-url>
   ```

4. Sync changes from upstream:
   ```bash
   git fetch upstream
   git merge upstream/main
   ```

---

## **17. Git Best Practices**

1. **Commit Often**: Make small, meaningful commits.  
2. **Write Descriptive Commit Messages**:  
   ```plaintext
   Fix login bug preventing OAuth sign-in
   ```
3. **Use Branches**: Feature, bugfix, and release branches.  
4. **Pull Before Push**: Avoid conflicts.  
5. **Review Code**: Use pull requests for collaboration.  

---

## **18. Help and Documentation**

### **Get Help**
```bash
git help <command>
git <command> --help
```

### **Git Documentation**
Official Git docs: [https://git-scm.com/doc](https://git-scm.com/doc)

---

This **Git cheat sheet** provides the essentials for version control, collaborative workflows, and efficient Git usage.
