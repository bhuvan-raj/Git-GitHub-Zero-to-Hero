<img src="https://github.com/bhuvan-raj/Git-GitHub-Zero-to-Hero/blob/main/assets/git.png" alt="Banner" />

<div align="center">

![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)

# Git Merge

> **Bring two branches together — cleanly, safely, and with a full understanding of what Git is doing.**

</div>

---

## 📋 Table of Contents

- [What is git merge?](#-what-is-git-merge)
- [How to Merge](#-how-to-merge)
- [Fast-Forward Merge](#-fast-forward-merge)
- [Three-Way (Recursive) Merge](#-three-way-recursive-merge)
- [Merge Conflicts](#-merge-conflicts)
- [Merge vs Rebase](#-merge-vs-rebase)
- [Merge Strategies](#-merge-strategies-advanced)
- [Quick Reference](#-quick-reference)

---

## 💡 What is git merge?

`git merge` integrates changes from one branch into another. When you execute a merge, Git takes the tips of two branches, finds their **common ancestor commit**, and combines the changes from both histories into the target branch.

---

## 🔀 How to Merge

The general workflow is always the same:

**Step 1** — Switch to the branch you want to merge **into** (the target):

```bash
git switch main
```

**Step 2** — Run the merge, specifying the **source** branch:

```bash
git merge feature-login
```

The `main` branch is updated with the changes from `feature-login`. The `feature-login` branch itself remains unaffected.

---

## ⚡ Fast-Forward Merge

<img src="https://github.com/bhuvan-raj/Git-GitHub-Zero-to-Hero/blob/main/assets/fastforward.png" alt="Fast Forward Merge" />

A **fast-forward merge** occurs when there is a **linear path** from the tip of the target branch to the tip of the source branch — meaning the target branch has not received any new commits since the source branch was created.

```
Before merge:
main:     A ── B
                \
feature:         C ── D ── E   ← (HEAD of feature-login)

After fast-forward merge:
main:     A ── B ── C ── D ── E   ← (main pointer moved forward)
```

**What happens:** Git simply moves the `main` pointer forward to `E`. No new commit is created. History stays perfectly linear and clean.

**When it happens:** When `main` has not diverged — no new commits were added to `main` after `feature-login` branched off.

**Force a merge commit even when fast-forward is possible:**

```bash
git merge --no-ff feature-login
```

This creates a merge commit for record-keeping, even though a fast-forward was possible. Useful when you want the branch history preserved in `git log`.

---

## 🔀 Three-Way (Recursive) Merge

<img src="https://github.com/bhuvan-raj/Git-GitHub-Zero-to-Hero/blob/main/assets/recursive.png" alt="Three Way Merge" />

A **three-way merge** occurs when both branches have **diverged** — new commits have been added to both the target and source branches since they split from their common ancestor.

```
Before merge:
main:     A ── B ── C ── F        ← F is a new commit on main
                \
feature:         D ── E           ← commits on feature branch

After three-way merge:
main:     A ── B ── C ── F ── M   ← M is a new merge commit
                \            /
feature:         D ── E ─────
```

**How Git does it:** Git uses **three commits** to calculate the result:
1. The tip of `main` (F)
2. The tip of `feature` (E)
3. Their **common ancestor** (C)

Git calculates what changed in each branch since the ancestor and combines both sets of changes. The result is a **new merge commit (M)** with two parents — F and E.

This merge commit is what makes `git log --graph` show the classic branch-and-merge structure.

---

## ⚠️ Merge Conflicts

A **conflict** occurs when Git cannot automatically decide how to combine changes because the **same lines in the same file** were modified differently in both branches since their common ancestor.

### When a conflict happens:

Git pauses the merge and marks the conflicting files. Your terminal shows:

```
Auto-merging app.py
CONFLICT (content): Merge conflict in app.py
Automatic merge failed; fix conflicts and then commit the result.
```

### What the conflict markers look like inside the file:

```
<<<<<<< HEAD
This is the version from the main branch (current branch).
=======
This is the version from the feature-login branch (being merged).
>>>>>>> feature-login
```

### How to resolve:

**Step 1** — Open the conflicted file and decide what the correct content should be. Edit the file to remove the `<<<<<<<`, `=======`, and `>>>>>>>` markers and keep the right code (or a combination of both).

**Step 2** — Stage the resolved file:

```bash
git add app.py
```

**Step 3** — Complete the merge:

```bash
git commit
# Git pre-fills the merge commit message — just save and close
```

### Abort the merge if you change your mind:

```bash
git merge --abort
```

Returns your repository to the state it was in before the merge attempt.

---

## ⚖️ Merge vs Rebase

| Feature | Merge | Rebase |
|---------|-------|--------|
| History | Preserved — non-linear, shows branches | Rewritten — linear, no merge commits |
| Merge Commit | ✅ Creates one (three-way) | ❌ No merge commit |
| Safety | ✅ Always safe | ⚠️ Risky on shared/public branches |
| Best For | Team collaboration, shared branches | Cleaning up local commits before PR |
| Command | `git merge feature` | `git rebase main` |

> ✅ **Rule:** Use `merge` for integrating work on shared branches. Use `rebase` only for cleaning up your own local commits before sharing them.

---

## 🧠 Merge Strategies (Advanced)

Git automatically picks the best strategy. These are the main ones:

| Strategy | When Used | Behavior |
|----------|-----------|---------|
| `recursive` | Default for two-branch merges | Standard three-way merge — handles renames and complex cases |
| `octopus` | Default for merging 3+ branches | Refuses if conflicts require manual resolution |
| `ours` | Manually specified | Result is always the current branch — ignores all incoming changes |
| `ff-only` | When you want to enforce no merge commits | Fails if a fast-forward is not possible |

```bash
# Merge only if fast-forward is possible — fail otherwise
git merge --ff-only feature-login

# Always create a merge commit, even if fast-forward is possible
git merge --no-ff feature-login
```

---

## 📌 Quick Reference

| Task | Command |
|------|---------|
| Merge a branch into current | `git merge <branch>` |
| Merge with explicit merge commit | `git merge --no-ff <branch>` |
| Fast-forward only merge | `git merge --ff-only <branch>` |
| Abort a merge in progress | `git merge --abort` |
| Stage resolved conflict file | `git add <file>` |
| Complete a merge after resolving | `git commit` |

---

<div align="center">

*Part of the [Git & GitHub Zero to Hero](../README.md) course*

</div>
