# Git Topic-wise Learning Plan

## 1. Introduction to Version Control and Git
- What is Version Control System (VCS)?
- Difference between Git and GitHub
- Centralized vs. Distributed VCS
- Installing Git

## 2. Git Configuration
- `git config` command
- Setting up username and email
  ```bash
  git config --global user.name "Your Name"
  git config --global user.email "you@example.com"
  ```
- Checking configurations:
  ```bash
  git config --list
  ```

## 3. Creating and Initializing a Repository
- `git init` – Initialize Git in a folder
- `git clone` – Copy remote repository

## 4. Basic Workflow
- `git status` – See current changes
- `git add` – Stage files
- `git commit` – Save changes with a message
  ```bash
  git add filename
  git commit -m "Initial commit"
  ```

## 5. Viewing Changes
- `git log` – View commit history
- `git diff` – Show file changes before commit
- `git show` – Show specific commit details

## 6. Branching and Merging
- Creating branches: `git branch feature-1`
- Switching branches: `git checkout feature-1`
- Merging branches:
  ```bash
  git checkout main
  git merge feature-1
  ```

## 7. Working with Remote Repositories (GitHub/GitLab)
- Add a remote:
  ```bash
  git remote add origin <repo-url>
  ```
- Push changes: `git push origin main`
- Pull updates: `git pull origin main`
- Clone repo: `git clone <repo-url>`

## 8. Undoing Changes
- `git checkout -- filename` – Undo local changes
- `git reset` – Unstage files
- `git revert` – Create a new commit to undo
- `git reset --hard` – Discard all changes (⚠️ destructive)

## 9. Git Stash
- Temporarily save work:
  ```bash
  git stash
  git stash apply
  git stash pop
  ```

## 10. Git Tags and Releases
- Create a tag: `git tag v1.0`
- Push tags: `git push origin v1.0`

## 11. Collaborating with Teams
- Forking repositories
- Pull Requests (PRs)
- Resolving merge conflicts
- Code reviews and Git best practices

## 12. Git Advanced Concepts
- Rebasing: `git rebase`
- Cherry-pick: `git cherry-pick <commit>`
- Git hooks
- Git submodules

## 13. Git GUIs and Tools
- GitHub Desktop
- Sourcetree
- VS Code Git integration


In Git, when you make changes to files and manage versions, those files pass through **three main areas** or **stages**:

---

### 🧱 **The Three Git Areas**

| Git Area                              | Description                                      |
| ------------------------------------- | ------------------------------------------------ |
| **1. Working Directory (Workspace)**  | Where you edit files. This is your local folder. |
| **2. Staging Area (Index)**           | Where you prepare changes before committing.     |
| **3. Repository (.git / Local Repo)** | Where committed changes are saved permanently.   |

---

### 🔄 **How Git Works (Step-by-Step Flow)**

```
[ Working Directory ] --> git add --> [ Staging Area ] --> git commit --> [ Local Repository ]
```

---

### 📂 1. **Working Directory**

* This is your actual project folder.
* Files here can be:

  * **Untracked** (Git doesn’t know about them yet)
  * **Modified** (but not staged)
* Run: `git status` to see file state

---

### 📥 2. **Staging Area (Index)**

* Temporary place where changes are stored before committing.
* Use `git add <filename>` to move changes here.
* Lets you commit only selected changes.

---

### 🗃️ 3. **Repository (Local Repo)**

* The `.git` folder where Git permanently stores your commits.
* Use `git commit -m "message"` to save changes from staging to here.
* This is your version history.

---

### 🔁 Bonus: **Remote Repository**

* Not part of the three core areas, but important.
* Stored on GitHub/GitLab/Bitbucket.
* Use `git push` to send commits to remote
* Use `git pull` to bring updates from remote

---

### 📌 Summary Diagram

```
Working Directory
     ↓ (git add)
Staging Area (Index)
     ↓ (git commit)
Local Repository (.git folder)
     ↓ (git push)
Remote Repository (GitHub, etc.)
```

---
Sure! Here's the **reverse flow of Git areas**, showing how code moves **backward** from remote to local editing:

---

### 🔄 **Git Flow (Backward Direction)**

```
[ Remote Repository ] ← git push / git pull → [ Local Repository ] ← git commit ← [ Staging Area ] ← git add ← [ Working Directory ]
```

---

### 🧭 **Step-by-Step Backward Explanation**

1. **Remote Repository (GitHub/GitLab)**

   * Central shared location for collaboration.
   * Use `git pull` to **fetch and merge** code into your local repo.

2. **Local Repository (.git folder)**

   * Stores committed history.
   * Use `git log` to view history.
   * Changes can be **reset**, **reverted**, or **rebased**.

3. **Staging Area (Index)**

   * Acts as a preview area before committing.
   * Use `git reset` to move changes **out** of staging.
   * Use `git restore --staged <file>` to **unstage** files.

4. **Working Directory**

   * Where you actually write and edit code.
   * You can discard changes using:

     ```bash
     git restore <file>
     ```
   * You can stash changes with:

     ```bash
     git stash
     ```

---

### 📌 Example Commands for Moving Backward

| Direction                  | Command                       |
| -------------------------- | ----------------------------- |
| Repo → Staging             | `git reset HEAD <file>`       |
| Staging → Working Dir      | `git restore --staged <file>` |
| Working Dir (undo changes) | `git restore <file>`          |
| Remote → Local             | `git pull origin main`        |

---

Great question! Understanding **when to use `git restore` vs `git reset`** helps you avoid accidental data loss and choose the right action for your need.

---

## 🆚 `git restore` vs `git reset` – **When to Use What?**

| Action                                               | Use `git restore`                | Use `git reset`              |         |          |
| ---------------------------------------------------- | -------------------------------- | ---------------------------- | ------- | -------- |
| 🔁 **Undo changes in working directory**             | ✅ Yes (`git restore <file>`)     | ❌ No                         |         |          |
| 🗃️ **Unstage a file (from staging to working dir)** | ✅ `git restore --staged <file>`  | ✅ `git reset <file>`         |         |          |
| 🧹 **Unstage all files**                             | ✅ `git restore --staged .`       | ✅ `git reset`                |         |          |
| 🔙 **Move commit pointer (undo commits)**            | ❌ No                             | ✅ \`git reset --soft         | --mixed | --hard\` |
| 🛑 **Discard all changes (dangerous)**               | ✅ `git restore .`                | ✅ `git reset --hard`         |         |          |
| 🧪 **Safe undo before commit**                       | ✅ Best for discarding file edits | ❌ Riskier for commit changes |         |          |

---

### 🛠️ **When to Use `git restore`**

Use `git restore` when:

* You want to **discard local file changes** before committing:

  ```bash
  git restore file.txt
  ```
* You want to **unstage** files but keep the changes:

  ```bash
  git restore --staged file.txt
  ```

✔️ Safe and recommended for file-level changes.

---

### 🧨 **When to Use `git reset`**

Use `git reset` when:

* You accidentally added files and want to **unstage** them:

  ```bash
  git reset file.txt
  ```
* You want to **undo commits** and move the HEAD (carefully):

  ```bash
  git reset --soft HEAD~1   # keep changes in staging
  git reset --mixed HEAD~1  # keep changes in working dir
  git reset --hard HEAD~1   # delete changes entirely
  ```

⚠️ Be cautious with `--hard`. It will **permanently delete changes**.

---

### ✅ Summary: Quick Decision Guide

| Goal                       | Command                                             |
| -------------------------- | --------------------------------------------------- |
| Unstage a file             | `git restore --staged <file>` or `git reset <file>` |
| Discard file changes       | `git restore <file>`                                |
| Undo last commit safely    | `git reset --soft HEAD~1`                           |
| Delete all changes (risky) | `git reset --hard`                                  |

---
### 📝 What is `git commit --amend` in Git?

The `git commit --amend` command is used to **modify the most recent commit**. It's helpful when you:

* Forgot to include a file in your last commit.
* Want to fix or update your last commit message.
* Need to make small corrections without creating a new commit.

---

### 🛠️ **How to Use `git commit --amend`**

#### 1. **Amend the last commit message only**

```bash
git commit --amend
```

> This opens your text editor (like Vim or VS Code) so you can edit the message.

#### 2. **Add a missed file to the last commit**

```bash
git add missed_file.txt
git commit --amend --no-edit
```

> This adds the new file into the **previous commit** without changing the message.

---

### ⚠️ When Should You Use `--amend`?

| Use Case                                         | Should You Use It? | Notes                                                       |
| ------------------------------------------------ | ------------------ | ----------------------------------------------------------- |
| 🧠 Forgot to add a file in the last commit       | ✅ Yes              | Stage the file, then amend                                  |
| ✍️ Want to change the commit message             | ✅ Yes              | Just run `git commit --amend`                               |
| 📦 Need to combine changes into one clean commit | ✅ Yes              | Used in cleanup before pushing                              |
| 🚀 Already pushed the commit to remote           | ⚠️ Careful!        | Requires `git push --force` and **can affect team members** |

---

### 💣 Be Careful With:

If you've already pushed the original commit to a shared remote, amending it and doing a **force push** may **break others' history**.

```bash
git push --force
```

🔄 What is git reset in Git?
git reset is a powerful Git command used to undo changes in your Git history or working directory. Depending on how it's used, it can:

  * Unstage files from the staging area (index)

  * Undo commits and move the HEAD

  * Change the state of your working directory



---

### ✅ Summary

| Goal                               | Command                                        |
| ---------------------------------- | ---------------------------------------------- |
| Edit last commit message           | `git commit --amend`                           |
| Add missing file to last commit    | `git add file && git commit --amend --no-edit` |
| Avoid extra commits during cleanup | `git commit --amend`                           |

---
* What is git clean -fd in Git?
The command git clean -fd is used to forcefully remove *untracked files* and directories from your working directory.




### 🔀 What is `git merge` in Git?

`git merge` is a Git command used to **combine changes** from one branch into another. It is essential in **collaborative development** where multiple branches are used (e.g., `feature`, `bugfix`, `main`).

---

### 📌 **Purpose of `git merge`:**

To integrate the **history and changes** from a source branch into your current branch.

---

### 🧠 **Basic Syntax:**

```bash
git merge <branch-name>
```

This merges `<branch-name>` **into your current branch**.

---

### ✅ **When Should You Use `git merge`?**

| Situation                                                       | Use `git merge`? | Example                            |
| --------------------------------------------------------------- | ---------------- | ---------------------------------- |
| Feature development complete and ready for integration          | ✅ Yes            | Merge `feature/login` into `main`  |
| You want to bring changes from a stable branch into your branch | ✅ Yes            | Merge `main` into `feature/login`  |
| Collaborating with others and want to combine efforts           | ✅ Yes            | Merge `teammate-branch` into yours |
| After resolving conflicts or reviewing changes                  | ✅ Yes            | Final merge for deployment         |
| To combine release branches                                     | ✅ Yes            | Merge `release/v1.0` into `main`   |

---

### 🔄 **How `git merge` Works:**

1. Move to the branch you want to merge **into**:

   ```bash
   git checkout main
   ```

2. Merge the target branch:

   ```bash
   git merge feature-branch
   ```

---

### 🔍 **Types of Merge:**

| Type                   | What It Does                                                 |
| ---------------------- | ------------------------------------------------------------ |
| **Fast-forward merge** | Directly moves the pointer if no new commits in base branch  |
| **Three-way merge**    | Combines changes when both branches have diverged            |
| **Merge conflict**     | Happens when changes conflict – Git asks you to resolve them |

---

### ⚔️ **Merge Conflict Example**

```bash
Auto-merging file.txt
CONFLICT (content): Merge conflict in file.txt
```

You must manually edit the file, then:

```bash
git add file.txt
git commit
```

---

### 🆚 Merge vs Rebase (Quick Note)

| Feature               | `git merge` | `git rebase`                      |
| --------------------- | ----------- | --------------------------------- |
| Keeps full history    | ✅ Yes       | ❌ Rewrites history                |
| Creates merge commits | ✅ Yes       | ❌ Linear history                  |
| Easier for teams      | ✅ Yes       | ⚠️ More risky for shared branches |

---

### 🧪 Example:

```bash
git checkout main
git merge feature-1
```

This integrates `feature-1` into `main`.

---

### ✅ Summary

| Use Case                                  | Should You Use `git merge`? |
| ----------------------------------------- | --------------------------- |
| Combine feature into main                 | ✅ Yes                       |
| Pull in updates from main to your feature | ✅ Yes                       |
| Maintain full commit history              | ✅ Yes                       |
| Resolve code conflicts manually           | ✅ Required                  |

---




