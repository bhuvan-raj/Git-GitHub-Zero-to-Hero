
<div align="center">

![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)

# Clone & Fork

> **Clone brings code to your machine. Fork brings it to your GitHub account. Together they power open-source contribution.**

</div>

---

## 📋 Table of Contents

- [git clone](#-git-clone)
- [GitHub Fork](#-github-fork)
- [Connection Diagram](#-connection-diagram)
- [Clone vs Fork Comparison](#-clone-vs-fork-comparison)
- [The Full Open-Source Contribution Workflow](#-the-full-open-source-contribution-workflow)

---

## 📥 git clone

### What it is

`git clone` **downloads a full copy of a GitHub repository** — including all files, branches, commit history, and tags — to your **local machine**.

After cloning, your local copy is connected to the original repository via a **remote** called `origin`.

### Command

```bash
git clone https://github.com/username/repository.git
```

### What happens when you clone

Git copies:
- All files in all branches
- Complete commit history
- All tags and remote tracking references
- A configured `origin` remote pointing back to the source URL

```bash
git clone https://github.com/nyrahul/wisecow.git

# Result: local folder created
wisecow/
  ├── .git/        ← full Git history
  ├── app.py
  ├── Dockerfile
  └── README.md
```

### Check the remote connection after cloning

```bash
git remote -v
# origin  https://github.com/nyrahul/wisecow.git (fetch)
# origin  https://github.com/nyrahul/wisecow.git (push)
```

### When to use git clone

| Scenario | Example |
|----------|---------|
| You are part of the same team | Clone the team repo, make changes, push directly |
| You want to study a codebase locally | Clone a public repo to read and experiment |
| You want a local backup | Clone to another machine for offline work |

---

## 🍴 GitHub Fork

### What it is

**Forking** creates a **copy of someone else's GitHub repository under your own GitHub account** — not just on your local machine.

Your fork is an **independent remote repository** that you fully own and control. It is linked to the original for the purpose of submitting Pull Requests back to it.

### How to fork

Click the **"Fork"** button in the top-right corner of any GitHub repository. GitHub creates:

```
Original: github.com/original-dev/project
Your fork: github.com/your-username/project   ← fully under your control
```

### Why fork?

| Scenario | Why Fork |
|----------|---------|
| Contribute to open source you don't own | Fork → change → PR back to original |
| Experiment without affecting the original | Your fork is completely independent |
| Build your own version of a public project | Fork and develop in your own direction |

---

## 🔗 Connection Diagram

```
       ┌──────────────────────────────┐
       │   Original Repository        │
       │   github.com/original/app    │
       └─────────────┬────────────────┘
                     │
                     │  Fork (GitHub button)
                     ▼
       ┌──────────────────────────────┐
       │   Your Forked Repository     │
       │   github.com/your-name/app   │
       └─────────────┬────────────────┘
                     │
                     │  git clone
                     ▼
       ┌──────────────────────────────┐
       │   Local Repository           │
       │   ~/projects/app             │
       └──────────────────────────────┘
```

---

## ⚖️ Clone vs Fork Comparison

| Feature | `git clone` | GitHub Fork |
|---------|------------|------------|
| Where copy is created | On your **local machine** | On your **GitHub account** |
| Connection to original | Points to same remote (`origin`) | Independent copy (linked for PRs) |
| Permissions required | Need write access to push back | No permission needed to fork |
| Typical use case | Team collaboration, local development | Open-source contribution, customization |
| How you do it | `git clone <url>` in terminal | Click "Fork" button on GitHub |
| Can create Pull Request? | Only if you have write access | Yes — from your fork to the original |
| Who owns the remote copy | The original repo owner | You own your fork |

---

## 🔄 The Full Open-Source Contribution Workflow

This is the standard workflow for contributing to any public project on GitHub when you do not have write access to the original repository:

### Step 1 — Fork the repository on GitHub

Click **Fork** on `github.com/original-dev/project`.

Your fork is now at `github.com/your-username/project`.

### Step 2 — Clone your fork to your local machine

```bash
git clone https://github.com/your-username/project.git
cd project
```

### Step 3 — Add the original repo as an upstream remote

This lets you pull future updates from the original project into your fork:

```bash
git remote add upstream https://github.com/original-dev/project.git

# Verify both remotes
git remote -v
# origin    https://github.com/your-username/project.git (fetch)
# origin    https://github.com/your-username/project.git (push)
# upstream  https://github.com/original-dev/project.git (fetch)
# upstream  https://github.com/original-dev/project.git (push)
```

### Step 4 — Create a new branch for your contribution

Never commit directly to `main`. Always use a dedicated branch:

```bash
git switch -c feature-fix-login-bug
```

### Step 5 — Make your changes and commit

```bash
# Edit files...
git add .
git commit -m "Fix null check in login validation"
```

### Step 6 — Push your branch to your fork

```bash
git push origin feature-fix-login-bug
```

### Step 7 — Open a Pull Request on GitHub

1. Go to your fork on GitHub — `github.com/your-username/project`
2. GitHub detects your new branch and shows a **"Compare & pull request"** button
3. Click it, fill in the PR title and description explaining what you changed and why
4. Submit the PR — it targets `original-dev/project:main`

The maintainers review your PR, request changes if needed, and merge it when ready.

### Step 8 — Keep your fork up to date

After your PR is merged (or anytime the original project has updates):

```bash
# Pull latest changes from the original
git fetch upstream
git switch main
git merge upstream/main

# Update your fork's main on GitHub
git push origin main
```

---

<div align="center">

*Part of the [Git & GitHub Zero to Hero](../README.md) course*

</div>
