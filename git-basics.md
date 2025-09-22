git basics starts with this :

1. first create a repository = use (git init ) to create a repo

2. after that if u want to add html,css and js in one step = use (touch index.html style.css script.js)

3. to check the username and user-email = use git config user.name and git config user.email

4. to make a directory = user mkdir (add-file name) = eg : mkdir git-folder

5. if u want to move a files to a folder = use mv  index.html style.css script.js project/

- mv = move
- project/ = target folder

eg : mv index.html style.css script.js git-folder/ 

6. if you u want to inspect history = use git log --oneline --all --graph

7. if u want to know difference between the last 2 commits u made = use git diff HEAD~1 HEAD

8. if u want to know the last commit details = use git show HEAD


9. if u want to create a branch = use git checkout g-b (new branch name) = eg : git -b feature

10. if u want to check the branches = use git branch 

11. if u want to delete a branch = use git branch -d (existing branch name) = eg : git -d OR D feature

12. if u want to rename a branch name = use git branch -M main = eg : main branch name is (master) => after using this master branch name will change into main branch name.

13. if u want to add git file to github first u need to connect with github repo :

- first step : git remote add origin https://github.com/username/practicing-git.git

-second step : 



14. if you want to merge a branch to the main branch = use git merge (mention the file name that you want to merge,) when u are merging the file don't merge the current file , for eg : if u want merge feature in main branch then mention => git merge feature in main branch as the current file.

15. if u want to checkout out in the old commits = > use git checkout (mention the previous id commit)

16. if u see a file in the normal stages section it means that the code is untracked.

17. Revert the merge:

git revert -m 1 <merge-commit-hash>


-m 1 tells Git to keep the first parent (main) and undo the changes from the merged branch.

This creates a new commit that undoes everything from that merge, including the file.


18. if u want to know where ur local repo is connected to remote repo = use git remote show origin

19. if u want to push ur file from local repo to remote repo = use git push -u origin main

20. if sync changes shows in the source control it means that if u have update anything in local repo they ask you to update in remote repo

21. if u want to add the main branch code to the default branch use git push (main branch name)

22.  the head gets detached from the main when u checkout through the deleted commits and u want and it will come to the main :

- when u enter this git checkout head , it will still detach from the main 
- when u enter this git checkout --hard head!~1 it will still detach from the main 

- so , therefore u have to add 2 or more commits and then prompt : git reset --hard head~2 , then point it to main branch

- then the head will attach to the main

23. git 

there are 3 methods to reset a commit u made :

1. git reset --hard, this method will delete the commit and put the head section to the previous main section
2. git reset --soft, by this method it will delete the commited changes and bring it back to the staged changes section
3. git reset , by this method it will delete the commited changes and bring it back to the changes section

4. if you want to recover or revert a commit that u have deleted u can find it by the
- first step : git reflog 
- second step : take the id of the commit u want to recover 
- third step : git --hard (enter the id);
- when u are using this method make sure that your code stays in the local and not push to the GitHub

5. git checkout head - this code will point out to the current directory u are

6. git checkout head~0 - this code will point out to the current directory u are

7. git checkout head~1 - head section will step down to the below directory from the current directory

8. git revert (id) - 

9. git revert head3..head

10. git revert --no-commit head~5 

11. git revert --continue => 	


12. if u want to revert 2 or more from above to below : use like this  = git revert head~3..head

13. if u want to revert 2 or more from above to below at once : use like this  = $ git revert --no-commit head~2..

14.  if u want to abort the commit use : git revert --abort

15. if u want to continue the commit : git revert --continue 

16. git merge --abort = is used when u pulled a remote branch to local branch and u want to undo the merge

Great question 🙌 — this is one of the most **important Git concepts** for teamwork. Let’s break it down clearly.

---

# 🔎 What is a Git conflict?

A **merge conflict** happens when Git cannot automatically decide **which changes to keep** during a merge, rebase, or cherry-pick.

This usually happens when:

* Two branches edit the **same line** in a file differently.
* Or one branch deletes a file while the other branch edits it.

---

## 📌 Example

You have a file `index.html`:

**On `main`:**

```html
<h1>Hello World</h1>
```

**On `feature`:**

```html
<h1>Hello Git</h1>
```

Now, when you try:

```bash
git checkout main
git merge feature
```

Git sees that **both changed the same line** → it can’t decide → **conflict**.

---

# 🛑 How Git shows a conflict

Inside the file, Git adds conflict markers:

```html
<<<<<<< HEAD
<h1>Hello World</h1>
=======
<h1>Hello Git</h1>
>>>>>>> feature
```

* `<<<<<<< HEAD` → your current branch’s version.
* `=======` → separator.
* `>>>>>>> feature` → the incoming branch’s version.

---

# ✅ How to Fix a Conflict

### 1. Open the file with conflicts

Look for `<<<<<<<`, `=======`, and `>>>>>>>`.

### 2. Choose how to resolve

You can:

* Keep your branch’s changes.
* Keep the other branch’s changes.
* **Combine/edit manually**.

Example fix:

```html
<h1>Hello World from Git</h1>
```

### 3. Mark as resolved

After editing, run:

```bash
git add index.html
```

### 4. Complete the merge

```bash
git commit
```

---

# ⚡ Tools to Help

* In **VS Code**, Git shows conflict sections with buttons:

  * “Accept Current Change”
  * “Accept Incoming Change”
  * “Accept Both Changes”
* In Git Bash, you’ll edit files manually.

---

# ✅ Summary

* **Git conflict** = Git doesn’t know which change to keep.
* Fix = manually edit the file, choose the correct code, then `git add` + `git commit`.

---

👉 Do you want me to make a **step-by-step practice exercise** where you intentionally create a conflict and then resolve it, so you can try it out locally?


Perfect timing 🚀 — these **stash commands** are very handy when working with Git. Let’s go step by step:

---

# 🔑 What is `git stash`?

`git stash` temporarily saves your **uncommitted changes** (both staged and unstaged) so you can work on something else without committing them.

Think of it like a **clipboard** for your changes.

---

## 📌 Main Stash Commands

### 1. `git stash`

* Saves your current changes and makes your working directory **clean** (like you just checked out the branch fresh).

```bash
git stash
```

Now your changes are hidden in the stash list.

---

### 2. `git stash list`

* Shows all saved stashes.

```bash
git stash list
```

Output example:

```
stash@{0}: WIP on main: 1234abc Added new feature
stash@{1}: WIP on feature: 5678def Fixed bug
```

---

### 3. `git stash apply`

* Applies a stash (by default the latest one) **without removing it** from the stash list.

```bash
git stash apply
```

Or apply a specific stash:

```bash
git stash apply stash@{1}
```

---

### 4. `git stash drop`

* Deletes a stash from the list.

```bash
git stash drop stash@{0}
```

---

### 5. `git stash clear`

* Removes **all stashes**. Be careful ⚠️.

```bash
git stash clear
```

---

## 📌 Workflow Example

1. You’re working on `index.html` but need to switch branches:

   ```bash
   git stash
   ```

   → Your changes are saved, working directory is clean.

2. Switch branches, do some work.

3. Come back, reapply your saved work:

   ```bash
   git stash apply
   ```

4. After confirming you no longer need it:

   ```bash
   git stash drop
   ```

---

## ⚡ Quick Analogy

* `git stash` = put changes in your **pocket**.
* `git stash list` = check your pockets.
* `git stash apply` = take changes out of your pocket but **leave a copy** inside.
* `git stash drop` = throw away one pocket.
* `git stash clear` = empty all pockets.

---

👉 Do you want me to also show you how to **stash only specific files or even untracked fil