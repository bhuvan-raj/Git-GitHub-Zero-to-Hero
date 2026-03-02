
<div align="center">

![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)

# Git Reset & Revert

> **Know how to undo in Git — and more importantly, know which tool to reach for.**

</div>

---

## 📋 Table of Contents

- [Overview](#-overview)
- [git reset](#-git-reset)
  - [The Three Modes](#the-three-modes)
  - [Reset Commands](#reset-commands)
- [git revert](#-git-revert)
  - [How It Works](#how-it-works)
  - [Revert Commands](#revert-commands)
- [Reset vs Revert — Full Comparison](#-reset-vs-revert--full-comparison)
- [Quick Reference](#-quick-reference)

---

## 🧭 Overview

Git gives you two main tools for undoing changes:

| Tool | What It Does | Safe on Shared Branches? |
|------|-------------|--------------------------|
| `git reset` | Moves HEAD backward — rewrites history | ⚠️ No |
| `git revert` | Creates a new commit that undoes a past commit | ✅ Yes |

The fundamental rule is simple: **Use `git reset` for local cleanup before pushing. Use `git revert` for undoing commits that are already shared.**

---

## 🔁 git reset

`git reset` moves the current branch's HEAD to a specified earlier commit. Depending on the mode used, it also affects the staging area and working directory.

### The Three Modes

Git reset has **three modes** — each controls how far the "reset" reaches across your three local Git areas:

```
             ┌──────────────────────┐
             │   Local Repository   │
             │  (Commits / HEAD)    │  ← HEAD always moves in all three modes
             └──────────┬───────────┘
                        │
             ┌──────────▼───────────┐
             │    Staging Area      │  ← affected by --mixed and --hard
             └──────────┬───────────┘
                        │
             ┌──────────▼───────────┐
             │  Working Directory   │  ← only affected by --hard
             └──────────────────────┘
```

| Mode | HEAD Moves | Staging Area | Working Directory | Use Case |
|------|-----------|-------------|-------------------|----------|
| `--soft` | ✅ Yes | ❌ Untouched | ❌ Untouched | Undo commit — keep changes staged ready to re-commit |
| `--mixed` *(default)* | ✅ Yes | ✅ Cleared | ❌ Untouched | Undo commit — unstage changes but keep edits in files |
| `--hard` | ✅ Yes | ✅ Cleared | ✅ Cleared | Completely discard commit and all changes |

---

### Reset Commands

#### Undo last commit — keep changes staged

```bash
git reset --soft HEAD~1
```

HEAD moves one commit back. All the changes from that commit remain in your staging area, ready to be re-committed with a corrected message or adjustments.

#### Undo last commit — unstage changes (most common)

```bash
git reset --mixed HEAD~1
# or simply:
git reset HEAD~1
```

HEAD moves one commit back. Changes come back to your working directory as **modified but unstaged** files. Nothing is lost — you just have to `git add` again before committing.

#### Undo last commit — discard all changes permanently

```bash
git reset --hard HEAD~1
```

> ⚠️ **Danger — irreversible.** HEAD moves back and all changes from that commit are permanently deleted from both staging area and working directory.

#### Unstage a specific file (without touching the commit)

```bash
git reset HEAD app.py
```

Removes `app.py` from the staging area but keeps your edits in the file. Equivalent to `git restore --staged app.py`.

#### Reset to a specific commit (not just one step back)

```bash
git reset --hard a1b2c3d
```

Moves HEAD to that exact commit SHA, discarding everything after it.

#### Recover from an accidental reset

If you reset too aggressively, Git stores the previous HEAD in `ORIG_HEAD`:

```bash
git reset --hard ORIG_HEAD
```

You can also use `git reflog` to find the SHA of any previous state and reset back to it.

---

## ↩️ git revert

`git revert` undoes the effect of a specific commit by **creating a brand new commit** that applies the inverse of the changes. It does **not** delete or rewrite any existing commits — history is preserved entirely.

> `git revert` = "undo by doing more commits"

### How It Works

Suppose your commit history is:

```
A ── B ── C ── D   ← HEAD (main)
```

If you run `git revert C`:

```
A ── B ── C ── D ── E   ← HEAD
```

Git creates commit `E` that **reverses exactly what `C` introduced**. Commit `C` still exists in the history — it is never touched. Commit `E` simply cancels out its effect.

---

### Revert Commands

#### Revert the most recent commit

```bash
git revert HEAD
```

Git creates a new commit undoing the last commit. An editor opens for the commit message — save and close to complete.

#### Revert a specific commit by SHA

```bash
git revert a1b2c3d
```

#### Revert without immediately opening the commit editor

```bash
git revert --no-edit a1b2c3d
```

Uses the default revert message automatically.

#### Revert but don't commit immediately (stage the changes only)

```bash
git revert --no-commit a1b2c3d
```

Stages the reverting changes without creating the commit — lets you review or combine with other changes before committing.

#### If a conflict occurs during revert

Git pauses and marks conflict areas in the file. Resolve them, then:

```bash
git add <resolved-file>
git revert --continue
```

#### Abort a revert in progress

```bash
git revert --abort
```

---

## ⚖️ Reset vs Revert — Full Comparison

| Feature | `git reset` | `git revert` |
|---------|------------|-------------|
| **How it undoes** | Moves HEAD backward — removes commits | Creates a new commit that reverses changes |
| **History** | ❌ Rewritten — commits are removed | ✅ Preserved — all commits remain |
| **Safe on shared branches** | ❌ No — rewrites history others depend on | ✅ Yes — safe to push |
| **Creates new commit** | ❌ No | ✅ Yes |
| **Affects working directory** | Depends on mode (`--hard` does) | No — only creates a commit |
| **Can undo a specific past commit** | Not directly — moves the whole branch tip | ✅ Yes — target any commit by SHA |
| **Best used for** | Local cleanup before `git push` | Undoing commits already pushed to a shared branch |

---

### When to use which

```
Have you pushed the commit to a shared remote?
│
├── NO  → Use git reset (--soft, --mixed, or --hard)
│          Safe to rewrite your local history
│
└── YES → Use git revert
           Creates a new undo commit — safe for everyone
```

---

## 📌 Quick Reference

| Action | Command |
|--------|---------|
| Undo commit, keep staged | `git reset --soft HEAD~1` |
| Undo commit, unstage (default) | `git reset HEAD~1` |
| Undo commit, discard changes | `git reset --hard HEAD~1` |
| Unstage a file | `git reset HEAD <file>` |
| Reset to specific commit | `git reset --hard <sha>` |
| Undo a bad reset | `git reset --hard ORIG_HEAD` |
| Revert last commit | `git revert HEAD` |
| Revert specific commit | `git revert <sha>` |
| Revert without editor prompt | `git revert --no-edit <sha>` |
| Abort a revert | `git revert --abort` |

---

<div align="center">

*Part of the [Git & GitHub Zero to Hero](../README.md) course*

</div>
