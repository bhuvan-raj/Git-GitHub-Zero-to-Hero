

<div align="center">

![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)

# Basic Git Commands

> **The commands you will use every single day — master these first.**

</div>

---

## 📋 Table of Contents

- [Starting a Repository](#-starting-a-repository)
- [Tracking Changes](#-tracking-changes)
- [Committing](#-committing)
- [Viewing History](#-viewing-history)
- [Comparing Changes with git diff](#-comparing-changes-with-git-diff)
- [Quick Reference](#-quick-reference)

---

## 🚀 Starting a Repository

### Initialize a new repository

```bash
git init
```

Creates a `.git/` folder in the current directory, turning it into a Git repository. Run this once at the start of a new project.

```bash
mkdir my-project
cd my-project
git init
# Initialized empty Git repository in /my-project/.git/
```

### Clone an existing repository

```bash
git clone https://github.com/username/repo.git
```

Downloads a full copy of a remote repository — all files, branches, and complete history — to your machine.

---

## 👀 Tracking Changes

### Check the status of your working directory

```bash
git status
```

Shows which files are untracked, modified, or staged. Run this constantly — it always tells you what Git knows about your project's current state.

```
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   app.py          ← staged ✅

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
        modified:   config.yml      ← modified but not staged

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        notes.txt                   ← new file, Git doesn't know about it yet
```

### Stage a specific file

```bash
git add file.txt
```

### Stage all changes in the current directory

```bash
git add .
```

### Stage parts of a file interactively (chunk by chunk)

```bash
git add -p file.txt
```

### Unstage a file (keep changes, remove from staging area)

```bash
git restore --staged file.txt
```

### Discard changes in working directory (irreversible — cannot undo)

```bash
git restore file.txt
```

> ⚠️ This permanently discards uncommitted local changes to `file.txt`. Use with caution.

---

## 📝 Committing

### Commit staged changes

```bash
git commit -m "your commit message"
```

Write commit messages that describe **what changed and why**, not how. Good examples:

```bash
git commit -m "Add user authentication via JWT"
git commit -m "Fix null pointer exception in payment service"
git commit -m "Refactor database connection pool settings"
```

### Skip staging — commit all modified tracked files directly

```bash
git commit -am "Quick fix for login redirect"
```

> ⚠️ The `-a` flag only includes files Git already tracks (previously committed). New untracked files still need `git add` first.

### Amend the last commit (before pushing)

Fix a typo in your last commit message or add a forgotten file:

```bash
git commit --amend -m "Corrected commit message"
```

> ⚠️ Never amend a commit that has already been pushed to a shared remote — it rewrites history and causes problems for teammates.

---

## 📜 Viewing History

### Show full commit history

```bash
git log
```

### Compact one-line format

```bash
git log --oneline
```

```
a1b2c3d Add user authentication
e4f5g6h Fix payment null pointer exception
7i8j9k0 Initial project setup
```

### Visual branch graph — most useful command for understanding your repo

```bash
git log --oneline --graph --decorate --all
```

```
*   3f2d1c4 (HEAD -> main) Merge branch 'feature-login'
|\
| * a2b3d4e (feature-login) Add login feature
* | 1a2b3c4 Fix config typo
|/
* 9b8c7d6 Initial project setup
```

### Show changes introduced by a specific commit

```bash
git show a1b2c3d
```

### Show who changed each line of a file

```bash
git blame file.txt
```

---

## 🔍 Comparing Changes with git diff

`git diff` shows exactly what changed — line by line — at different stages of your work.

### The Three Git Areas and Where diff Fits

```
             ┌────────────────────────────┐
             │        Repository          │
             │     (Last commit - HEAD)   │
             └────────────┬───────────────┘
                          ▲
                          │  git diff --staged
                          │  (Staging Area ↔ Last Commit)
                          │
             ┌────────────┴───────────────┐
             │        Staging Area        │
             │    (Files you git add-ed)  │
             └────────────┬───────────────┘
                          ▲
                          │  git diff
                          │  (Working Dir ↔ Staging Area)
                          │
             ┌────────────┴───────────────┐
             │     Working Directory      │
             │  (Your actual files now)   │
             └────────────────────────────┘
```

### Show unstaged changes (working directory vs staging area)

```bash
git diff
```

Shows what you have changed but **not yet staged** with `git add`.

### Show staged changes (staging area vs last commit)

```bash
git diff --staged
```

Shows what **will be included** in your next `git commit` — your staged changes compared against HEAD.

### Show changes between two commits

```bash
git diff a1b2c3d e4f5g6h
```

### Show changes between two branches

```bash
git diff main feature-login
```

### diff Command Summary

| Command | Compares | Shows |
|---------|---------|-------|
| `git diff` | Working Directory ↔ Staging Area | What you changed but haven't staged yet |
| `git diff --staged` | Staging Area ↔ Last Commit (HEAD) | What's staged and will go into the next commit |
| `git diff <hash1> <hash2>` | Two specific commits | What changed between those two points |
| `git diff <branch1> <branch2>` | Two branches | Difference between the tips of each branch |

---

## 📌 Quick Reference

| Task | Command |
|------|---------|
| Start a new repository | `git init` |
| Clone a remote repo | `git clone <url>` |
| Check current status | `git status` |
| Stage a specific file | `git add file.txt` |
| Stage all changes | `git add .` |
| Commit staged changes | `git commit -m "message"` |
| Stage + commit tracked files | `git commit -am "message"` |
| Amend last commit | `git commit --amend -m "new message"` |
| View commit history (visual) | `git log --oneline --graph --all` |
| See unstaged changes | `git diff` |
| See staged changes | `git diff --staged` |
| Unstage a file | `git restore --staged file.txt` |
| Discard working dir changes | `git restore file.txt` |

---

<div align="center">

*Part of the [Git & GitHub Zero to Hero](../README.md) course*

</div>
