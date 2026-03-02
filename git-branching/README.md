<img src="https://github.com/bhuvan-raj/Git-GitHub-Zero-to-Hero/blob/main/assets/git.png" alt="Banner" />

<div align="center">

![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)

# Git Branching

> **Branches let you work on new features without breaking what already works.**

</div>

---

## 📋 Table of Contents

- [What is a Branch?](#-what-is-a-branch)
- [Branch Commands](#-branch-commands)
- [Visualizing Branches](#-visualizing-branches)
- [Branching Workflow Example](#-branching-workflow-example)
- [Quick Reference](#-quick-reference)

---

## 💡 What is a Branch?

A **branch** in Git is a lightweight, movable pointer to a specific commit. The default branch is called `main` (or `master` in older repositories).

Think of branches as **parallel storylines in a book**. The `main` branch is the published story — always stable and production-ready. When you want to try a new idea (feature), you create a new branch. If the idea works, you merge it back. If it doesn't, you discard the branch — the main story is completely unaffected.

```
main:    A ── B ── C ──────────── G  (merge)
                    \            /
feature:             D ── E ── F
```

Branches allow teams to:
- Develop features in isolation without affecting stable code
- Work in parallel — multiple developers on different features simultaneously
- Experiment freely — discard branches that don't work out
- Maintain multiple release versions

---

## 🌿 Branch Commands

### List all local branches

```bash
git branch
```

The branch marked with `*` is your current branch (HEAD):

```
* main
  feature-login
  bugfix-payment
```

### Create a new branch

```bash
git branch feature-login
```

Creates the branch but **does not switch to it**. You remain on your current branch.

### Switch to a branch

```bash
git switch feature-login
```

Classic syntax (also works):

```bash
git checkout feature-login
```

### Create and switch in one step ⭐ Most used

```bash
git switch -c feature-login
```

Classic syntax:

```bash
git checkout -b feature-login
```

### Rename the current branch

```bash
git branch -m new-name
```

### Delete a branch (safe — only works if merged)

```bash
git branch -d feature-login
```

Git prevents deletion if the branch has unmerged changes, protecting your work.

### Force delete a branch (even if not merged)

```bash
git branch -D feature-login
```

> ⚠️ Use force delete only when you are certain you want to discard the branch's work permanently.

### List all branches including remote-tracking

```bash
git branch -a
```

```
* main
  feature-login
  remotes/origin/main
  remotes/origin/feature-login
```

### Push a new branch to remote

```bash
git push -u origin feature-login
```

The `-u` flag sets the upstream tracking — future `git push` and `git pull` from this branch will automatically know which remote branch to use.

### Delete a remote branch

```bash
git push origin --delete feature-login
```

---

## 🌳 Visualizing Branches

The best command for seeing your branch structure:

```bash
git log --oneline --graph --decorate --all
```

Example output:

```
*   3f2d1c4 (HEAD -> main) Merge branch 'feature-login'
|\
| * a2b3d4e (feature-login) Add login form validation
| * c1d2e3f Add login route
* | 8g9h0i1 Fix homepage typo
|/
* 7j8k9l0 Initial project setup
```

Reading the graph:
- `*` = a commit
- `|` = a branch line
- `\` or `/` = branching or merging point
- `HEAD ->` = your current position
- Names in `()` = branch or tag labels

---

## 🔁 Branching Workflow Example

A typical feature branch development workflow:

```bash
# 1. Start from an up-to-date main branch
git switch main
git pull origin main

# 2. Create and switch to a new feature branch
git switch -c feature-user-profile

# 3. Make your changes and commit
git add .
git commit -m "Add user profile page"

git add .
git commit -m "Style profile page with CSS"

# 4. Push the branch to remote for review / PR
git push -u origin feature-user-profile

# 5. After PR approval — merge back to main
git switch main
git merge feature-user-profile

# 6. Clean up — delete the branch locally and remotely
git branch -d feature-user-profile
git push origin --delete feature-user-profile
```

---

## 📌 Quick Reference

| Task | Command |
|------|---------|
| List local branches | `git branch` |
| List all branches (including remote) | `git branch -a` |
| Create a branch | `git branch <name>` |
| Switch to a branch | `git switch <name>` |
| Create and switch | `git switch -c <name>` |
| Rename current branch | `git branch -m <new-name>` |
| Delete merged branch | `git branch -d <name>` |
| Force delete branch | `git branch -D <name>` |
| Push branch to remote | `git push -u origin <name>` |
| Delete remote branch | `git push origin --delete <name>` |
| Visualize branch graph | `git log --oneline --graph --decorate --all` |

---

<div align="center">

*Part of the [Git & GitHub Zero to Hero](../README.md) course*

</div>
