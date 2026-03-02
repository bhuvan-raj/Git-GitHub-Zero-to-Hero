<img src="https://github.com/bhuvan-raj/Git-GitHub-Zero-to-Hero/blob/main/assets/gitarchitecture.png" alt="Banner" />

<div align="center">

![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)

# Git Architecture

> **Understand the four areas Git uses to track your work — and how files move between them.**

</div>

---

## 📋 Table of Contents

- [The Four Areas](#-the-four-areas)
- [Architecture Diagram](#-architecture-diagram)
- [Command and Data Flow](#-command-and-data-flow)
- [File States in Git](#-file-states-in-git)
- [The .git Directory](#-the-git-directory)

---

## 🗺️ The Four Areas

Git organizes your work across **four distinct areas**. Understanding these is the key to understanding every Git command.

### 1. Working Directory (Working Tree)

Your project files as they exist on disk — the files you see and edit in your code editor. When you modify a file, it becomes **modified** in the working directory.

### 2. Staging Area (Index)

A preparation zone between your working directory and your local repository. You selectively add changes here using `git add`. Only what is in the staging area gets included in the next commit.

Think of it as a **shopping cart** — you pick exactly what you want before checking out.

### 3. Local Repository (.git folder)

The permanent store of all your commits, branches, tags, and history. Created when you run `git init`. All history lives here as compressed SHA-1 objects — Git never loses a committed snapshot.

### 4. Remote Repository

A repository hosted on a platform like **GitHub, GitLab, or Bitbucket**. Used for sharing code and team collaboration. You push your local commits up to the remote and pull others' commits down.

---

## 🏗️ Architecture Diagram

```
  ┌─────────────────────────────────────────────────────────────────────┐
  │                        YOUR MACHINE                                 │
  │                                                                     │
  │  ┌──────────────────┐   git add    ┌──────────────────┐            │
  │  │  Working         │ ──────────▶  │  Staging Area    │            │
  │  │  Directory       │              │  (Index)         │            │
  │  │                  │ ◀──────────  │                  │            │
  │  │  your files      │  git restore │  changes ready   │            │
  │  │  as you edit     │  --staged    │  to be committed │            │
  │  └──────────────────┘              └────────┬─────────┘            │
  │           │                                 │                      │
  │           │  git restore                    │  git commit          │
  │           │  (discard edits)                │                      │
  │           │                                 ▼                      │
  │           │                        ┌──────────────────┐            │
  │           └───────────────────────▶│  Local Repo      │            │
  │                                    │  (.git folder)   │            │
  │                                    │                  │            │
  │                                    │  all commits     │            │
  │                                    │  and history     │            │
  │                                    └────────┬─────────┘            │
  └─────────────────────────────────────────────┼──────────────────────┘
                                                │
                                   git push ────┤
                                                │──── git pull / git fetch
                                                │
                                                ▼
                                   ┌──────────────────────┐
                                   │  Remote Repository   │
                                   │  (GitHub / GitLab)   │
                                   │                      │
                                   │  shared with team    │
                                   └──────────────────────┘
```

---

## 🔄 Command and Data Flow

```
Working Directory → (git add) → Staging Area → (git commit) → Local Repo → (git push) → Remote
        ▲                                                           │
        └───────────────────── git pull / git checkout ────────────┘
```

| Command | Movement |
|---------|---------|
| `git add` | Working Directory → Staging Area |
| `git restore --staged` | Staging Area → Working Directory (unstage) |
| `git commit` | Staging Area → Local Repository |
| `git restore` | Local Repo → Working Directory (discard changes) |
| `git push` | Local Repository → Remote Repository |
| `git pull` | Remote Repository → Local Repository + Working Directory |
| `git fetch` | Remote Repository → Local Repository only (no merge) |

---

## 📄 File States in Git

A file in your working directory can be in one of these states:

```
  Untracked ──▶ git add ──▶ Staged ──▶ git commit ──▶ Committed (Unmodified)
                                                              │
                                                    edit file │
                                                              ▼
                                                          Modified
                                                              │
                                                    git add   │
                                                              ▼
                                                           Staged
```

| State | Meaning |
|-------|---------|
| **Untracked** | New file Git has never seen — not in any commit or staging area |
| **Staged** | File has been `git add`-ed and is ready for the next commit |
| **Modified** | File was previously committed but has been changed — not yet staged |
| **Committed / Unmodified** | File matches its last committed snapshot exactly |

---

## 📁 The .git Directory

When you run `git init`, Git creates a hidden `.git/` folder in your project root. This is the **local repository** — everything Git needs to manage your project lives here.

```
.git/
├── HEAD          ← Points to the current branch
├── config        ← Repository-level config (local settings)
├── index         ← The staging area (binary file)
├── objects/      ← All commits, files, trees stored as compressed SHA-1 objects
│   ├── pack/
│   └── xx/
├── refs/
│   ├── heads/    ← Branch pointers (each branch = one file containing a commit SHA)
│   └── tags/     ← Tag pointers
└── logs/         ← History of HEAD and branch movements (used by git reflog)
```

> ⚠️ Never manually edit files inside `.git/` — Git manages this directory entirely. You interact with it only through Git commands.

---

<div align="center">

*Part of the [Git & GitHub Zero to Hero](../README.md) course*

</div>
