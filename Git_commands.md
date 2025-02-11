# Git Commands Cheat Sheet

## 1. **Initialization**
- **Initialize a new Git repository:**
  ```bash
  git init
  ```
  
- **Clone an existing repository:**
  ```bash
  git clone <repository_url>
  ```

## 2. **Staging and Committing**
- **Add a specific file to the staging area:**
  ```bash
  git add <filename>
  ```
- **Add all files to the staging area:**
  ```bash
  git add .
  ```
- **Commit changes with a message:**
  ```bash
  git commit -m "Your commit message"
  ```
- **Commit all changes (tracked files):**
  ```bash
  git commit -a -m "Your commit message"
  ```

## 3. **Pushing Changes**
- **Push changes to the default remote repository (origin) and branch:**
  ```bash
  git push
  ```
- **Push to a specific remote repository and branch:**
  ```bash
  git push origin <branch_name>
  ```
- **Force push (use with caution):**
  ```bash
  git push --force
  ```

## 4. **Pulling Changes**
- **Pull the latest changes from the remote repository:**
  ```bash
  git pull
  ```
- **Pull from a specific branch:**
  ```bash
  git pull origin <branch_name>
  ```

## 5. **Deleting**
- **Delete a file from the repository and the working directory:**
  ```bash
  git rm <filename>
  git commit -m "Remove <filename>"
  git push
  ```
- **Delete a branch locally:**
  ```bash
  git branch -d <branch_name>      # Safe delete
  git branch -D <branch_name>      # Force delete
  ```
- **Delete a remote branch:**
  ```bash
  git push origin --delete <branch_name>
  ```

## 6. **Managing Cache**
- **Remove a file from the staging area (cache) without deleting it locally:**
  ```bash
  git rm --cached <filename>
  git commit -m "Remove <filename> from cache"
  git push
  ```
- **Clear the entire Git cache:**
  ```bash
  git rm -r --cached .
  git add .
  git commit -m "Clear Git cache"
  git push
  ```

## 7. **Branch Management**
- **Create a new branch:**
  ```bash
  git branch <new_branch_name>
  ```
- **Switch to another branch:**
  ```bash
  git checkout <branch_name>
  ```
- **Create and switch to a new branch:**
  ```bash
  git checkout -b <new_branch_name>
  ```
- **Merge a branch into the current branch:**
  ```bash
  git merge <branch_name>
  ```

## 8. **Viewing Changes and History**
- **Check the status of the working directory:**
  ```bash
  git status
  ```
- **View commit history:**
  ```bash
  git log
  ```
- **View a concise, one-line log:**
  ```bash
  git log --oneline
  ```
- **View changes made to files:**
  ```bash
  git diff
  ```

## 9. **Undoing Changes**
- **Unstage a file:**
  ```bash
  git reset HEAD <filename>
  ```
- **Discard changes in the working directory:**
  ```bash
  git checkout -- <filename>
  ```
- **Revert a commit (create a new commit that undoes the changes):**
  ```bash
  git revert <commit_hash>
  ```

## 10. **Working with Remotes**
- **Add a remote repository:**
  ```bash
  git remote add origin <repository_url>
  ```
- **View remote repositories:**
  ```bash
  git remote -v
  ```
- **Remove a remote:**
  ```bash
  git remote remove <remote_name>
  ```

---

Keep this guide handy for quick reference while working with Git!

