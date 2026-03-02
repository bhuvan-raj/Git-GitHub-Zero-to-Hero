<img src="https://github.com/bhuvan-raj/Git-GitHub-Zero-to-Hero/blob/main/assets/git.png" alt="Banner" />

<div align="center">

![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)

# Git Stash

> **Put your work-in-progress in a safe locker and come back to it later — without committing half-done code.**

</div>

---

## 📋 Table of Contents

- [What is Git Stash?](#-what-is-git-stash)
- [When to Use Git Stash](#-when-to-use-git-stash)
- [How Git Stash Works Internally](#-how-git-stash-works-internally)
- [All Stash Commands](#-all-stash-commands)
- [Workflow Example](#-workflow-example)
- [apply vs pop](#-apply-vs-pop)
- [Real-World Use Cases](#-real-world-use-cases)
- [Pro Tips](#-pro-tips)
- [Quick Reference](#-quick-reference)

---

## 💡 What is Git Stash?

`git stash` **temporarily saves your uncommitted changes** — both staged and unstaged — and reverts your working directory to a clean state (matching the last commit), so you can switch context without losing your work.

Think of it like a **temporary locker** at a train station — you put your bags in when you need your hands free, and pick them back up when you return.

---

## 🧩 When to Use Git Stash

Use `git stash` when:

- You have **uncommitted changes** but need to **switch branches** urgently
- You want to **pull updates** from remote but your working directory is dirty
- You need to **quickly test something** without committing your current modifications
- You want to **temporarily set aside** work to focus on a higher-priority task

---

## ⚙️ How Git Stash Works Internally

When you run `git stash`, Git:

1. Takes all changes from the **working directory** (unstaged) and **staging area** (staged)
2. Saves them as a **new stash object** inside `.git/refs/stash`
3. Reverts your working directory to the **last committed state** — giving you a clean slate

Each stash is stored internally as **two commits**:
- One for the working directory changes
- One for the staged changes

Stashes are organized as a **stack** — last in, first out.

---

## 💻 All Stash Commands

### Save changes to a stash

```bash
git stash
```

Saves both staged and unstaged changes. Does **not** stash untracked files (new files not yet `git add`-ed) by default.

Add a descriptive message (always recommended):

```bash
git stash push -m "WIP: fixing login bug"
```

### Include untracked files

```bash
git stash -u
# or
git stash --include-untracked
```

### Include both untracked and ignored files

```bash
git stash -a
# or
git stash --all
```

---

### List all stashes

```bash
git stash list
```

```
stash@{0}: WIP on main: 34a9f12 Added login validation
stash@{1}: On dev: WIP on API refactor
```

Each stash entry has an index (`{0}`, `{1}`), the branch it was created on, and the commit it was based on.

---

### Apply the most recent stash (keeps stash in list)

```bash
git stash apply
```

### Apply a specific stash

```bash
git stash apply stash@{2}
```

> ⚠️ `apply` does **not** remove the stash from the list. Use `pop` if you want to apply and delete in one step.

---

### Apply and remove the most recent stash

```bash
git stash pop
```

### Apply and remove a specific stash

```bash
git stash pop stash@{1}
```

---

### View what's inside a stash

```bash
git stash show            # summary
git stash show -p         # full diff
```

---

### Delete a specific stash

```bash
git stash drop stash@{0}
```

### Delete all stashes

```bash
git stash clear
```

> ⚠️ `git stash clear` cannot be undone — all stashed work is permanently deleted.

---

### Create a new branch from a stash

```bash
git stash branch fix-login-bug stash@{0}
```

This creates a new branch, checks it out, applies the stash on it, and removes the stash entry — all in one command. Useful when your stashed work has grown large and deserves its own branch.

---

## 🔁 Workflow Example

You are on `main` working on a new feature when an urgent bug fix is needed on another branch:

```bash
# 1. You have uncommitted changes — save them
git stash push -m "WIP: feature update"

# 2. Switch to the bugfix branch safely
git switch bugfix-branch

# 3. Fix the bug and commit
git add .
git commit -m "Fix critical production bug"

# 4. Come back to your feature work
git switch main

# 5. Restore your stashed changes
git stash pop
```

Your feature work is right where you left it, as if nothing happened.

---

## ⚖️ apply vs pop

| Command | Reapplies Changes | Removes Stash from List | Use When |
|---------|-----------------|------------------------|----------|
| `git stash apply` | ✅ Yes | ❌ No | You want to keep the stash for reuse or safety |
| `git stash pop` | ✅ Yes | ✅ Yes | You are done with the stash and want it cleaned up |

---

## 🧩 Real-World Use Cases

| Scenario | Command | Why |
|----------|---------|-----|
| Need to switch branches mid-work | `git stash` | Keeps work safe, allows switching |
| Stash includes new files too | `git stash -u` | Includes untracked files |
| Save work with a clear label | `git stash push -m "WIP: login page"` | Easier to identify later |
| Recover changes after coming back | `git stash list` + `git stash pop` | Brings back stashed work |
| Move stashed work to a new branch | `git stash branch <name>` | Creates an isolated workspace for it |

---

## 🧠 Pro Tips

- Always use meaningful messages: `git stash push -m "WIP: Login page update"` — makes `git stash list` readable
- Avoid excessive stashing — if work is long-term, commit it to a temporary branch instead
- Use `git stash show -p > patch.diff` to export stashed changes as a patch file
- Use `git stash --keep-index` to stash only the **unstaged** changes, leaving staged changes intact

---

## 📌 Quick Reference

| Action | Command |
|--------|---------|
| Save work | `git stash` |
| Save with message | `git stash push -m "message"` |
| Include untracked files | `git stash -u` |
| List stashes | `git stash list` |
| View stash contents | `git stash show -p` |
| Apply latest (keep stash) | `git stash apply` |
| Apply and remove stash | `git stash pop` |
| Apply specific stash | `git stash apply stash@{n}` |
| Delete specific stash | `git stash drop stash@{n}` |
| Delete all stashes | `git stash clear` |
| Create branch from stash | `git stash branch <branch-name>` |

---

<div align="center">

*Part of the [Git & GitHub Zero to Hero](../README.md) course*

</div>
