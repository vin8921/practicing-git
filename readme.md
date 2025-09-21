# Git & GitHub — Step-by-step practice guide (using a single file `notes.txt`)

**Goal:** Practice and master Git & GitHub by repeatedly performing common workflows using one simple file (`notes.txt`). This builds muscle memory for commands, branching, merging, undoing, remotes, conflicts, and PRs.

---

## Prerequisites

* Git installed (run `git --version`).
* A GitHub account.
* Optional but recommended: VS Code or any code editor, GitHub web UI, and GitHub CLI (`gh`).

---

## Quick setup (do once)

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
# optional nice defaults
git config --global core.editor "code --wait"
```

---

## Part A — Local repository basics

### 1. Create a working folder and initialize

```bash
mkdir git-practice
cd git-practice
git init
```

### 2. Create your file and make the first commit

```bash
# create a normal file
echo "Day 1: learning git" > notes.txt
git status
git add notes.txt
git commit -m "chore: add notes.txt with Day 1 entry"
```

**What to observe:** `git status` (untracked -> staged -> committed). `git log --oneline` (shows your commit).

### 3. Edit and commit again

```bash
# edit the file using any editor or with echo >>
echo "Day 2: practicing commits" >> notes.txt
git add notes.txt
git commit -m "docs: add Day 2 note"
```

### 4. Inspect history and differences

```bash
git log --oneline --graph --decorate
git diff HEAD~1 HEAD   # difference between last two commits
git show HEAD          # show last commit details
```

### 5. Undo an unstaged change

```bash
# make an edit but don't add
echo "temp line" >> notes.txt
# discard local change
git restore notes.txt     # (modern) or: git checkout -- notes.txt
```

---

## Part B — Branching & merging practice

### 6. Create a feature branch and work there

```bash
git checkout -b feature/add-todo
echo "Day 3: feature work" >> notes.txt
git add notes.txt
git commit -m "feat: add Day 3 note"
```

### 7. Switch back and merge

```bash
git checkout main
git merge feature/add-todo
# if fast-forward, main simply moves forward
```

**Practice:** repeat with multiple commits on the feature branch so merges are non-trivial. Use `git merge --no-ff` to force a merge commit if you prefer a recorded merge.

### 8. Delete the branch after merge

```bash
git branch -d feature/add-todo
```

---

## Part C — Remote: GitHub push & pull

### 9. Create a repo on GitHub (web UI)

* Go to GitHub → New repository → give name `git-practice` → *Do not* initialize with README if you already have local commits.

### 10. Add remote & push

```bash
git remote add origin https://github.com/your-username/git-practice.git
git branch -M main              # ensure branch is main
git push -u origin main         # push initial commits and set upstream
```

### 11. Clone the repo (simulate a collaborator)

```bash
# move out of current folder
cd ..
git clone https://github.com/your-username/git-practice.git clone-test
cd clone-test
cat notes.txt
```

**Practice:** make small edits in `clone-test`, commit and push; then `git pull` in the original folder to sync.

---

## Part D — Feature branch + Pull Request flow (collaboration)

### 12. Create a branch, push it, and open a PR

```bash
git checkout -b feature/add-day4
echo "Day 4: PR flow" >> notes.txt
git add notes.txt
git commit -m "feat: add Day 4 note"
git push -u origin feature/add-day4
```

* Open GitHub → your repository → you should see a banner to open a Pull Request. Create the PR and merge via the web UI.

**Practice variations:** request changes in PR, add new commits to the same branch, push again, and complete the PR.

---

## Part E — Undoing and rewriting history (safe vs dangerous)

### 13. Revert a commit (safe for shared branches)

```bash
# find the commit hash with git log
git revert <commit-hash>
# this creates a new commit that undoes the specified commit
```

### 14. Reset (dangerous on shared branches)

```bash
# move HEAD back one commit but keep changes staged
git reset --soft HEAD~1
# or throw away changes completely (dangerous!):
git reset --hard HEAD~1
```

> **Warning:** `git reset --hard` and force pushing rewrite history — avoid on `main` or shared branches.

### 15. Amend the last commit (useful locally)

```bash
# change last commit message or content
git add notes.txt
git commit --amend -m "fix: correct Day 4 note"
```

If you already pushed the commit, you will need to force push: `git push --force-with-lease` (use with extreme caution).

---

## Part F — Conflicts & Stashing

### 16. Simulate & resolve a merge conflict

1. Create branch `branch-A` and change a single line in `notes.txt`, commit and push.
2. Create branch `branch-B` (from main) and change the same line differently, commit.
3. Merge `branch-B` into `main` then try to merge `branch-A` → you will get a conflict.

Resolve steps:

```bash
# open notes.txt, edit to resolve conflict (choose the correct content)
git add notes.txt
git commit   # finishes the merge after resolving
```

### 17. Stash your work

```bash
# you have uncommitted changes but need to switch branches
git stash push -m "WIP: experimenting"
# list stash
git stash list
# restore
git stash pop   # or git stash apply
```

---

## Part G — Tags, releases and small advanced tips

* Create an annotated tag: `git tag -a v1.0 -m "release v1.0"`
* Push tags: `git push origin v1.0` or `git push --tags`
* Interactive rebase (clean commits): `git rebase -i HEAD~3` (careful when rewriting shared history)

---

## Part H — Common commands cheat-sheet

```
git init
git clone <url>
git status
git add <file>
git commit -m "msg"
git log --oneline --graph --decorate
git checkout -b feature
git checkout main
git merge feature
git remote add origin <url>
git push -u origin main
git push origin feature
git pull
git revert <commit>
git reset --soft|--mixed|--hard <ref>
git stash push -m "msg"
git stash pop
git tag -a v1.0 -m "msg"
```

---

## Best practices (from day 1)

* Make **small, atomic commits** with meaningful messages (prefixes like `feat:`, `fix:`, `docs:` help).
* Use a branch per feature/bugfix.
* Pull frequently to avoid big merge conflicts.
* Don’t rewrite history on shared branches. Use `revert` on `main` for safe undos.
* Add a `.gitignore` for node\_modules, build artifacts, etc.
* Review your PRs and use CI (GitHub Actions) if possible.

---

## Practice plan (10 days to a month — progressive)

**Week 1 (days 1–7)**

* Day 1: Init repo, add notes.txt, commit twice.
* Day 2: Learn `git log`, `git diff`, `git restore`.
* Day 3: Branch, commit on branch, merge to main.
* Day 4: Create GitHub repo and push main.
* Day 5: Clone repo, make edits and push.
* Day 6: Create branch, open PR, merge via web UI.
* Day 7: Revert a commit and practice `reset` on a disposable branch.

**Week 2 (days 8–14)**

* Simulate merge conflicts and resolve them.
* Practice stash, apply, and pop.
* Practice tags and releases.
* Try `commit --amend` and `rebase -i` on branches that are not pushed.

**Beyond**: contribute to a small open-source repo, or pair with a friend and practice PR review.

---

## Short challenges (for mastery)

1. Make 10 tiny commits, squash them into 2 with an interactive rebase.
2. Create a branch, push it, create a PR, request changes, update the branch and finish the PR.
3. Create a conflicting change and fix it without losing any intended content.
4. Use `git revert` to undo a public commit; confirm history is preserved.

---

If you want, I can also:

* Provide a ready-to-run shell script that performs the local steps automatically (for practice), or
* Create a printable PDF of this guide, or
* Walk you through each command in your terminal interactively (you paste outputs and I explain).

---

*Happy practicing — small repeated actions build mastery. Keep committing!*

