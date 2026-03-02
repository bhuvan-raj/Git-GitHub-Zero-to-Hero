<img src="https://github.com/bhuvan-raj/Git-GitHub-Zero-to-Hero/blob/main/assets/git.png" alt="Banner" />

<div align="center">

![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)

# What is Version Control?

> **Stop naming files `project_final_FINAL_v3.zip`. Let Git handle history.**

</div>

---

## 📋 Table of Contents

- [What is a Version Control System?](#-what-is-a-version-control-system)
- [Centralized VCS (CVCS)](#-centralized-vcs-cvcs)
- [Distributed VCS (DVCS)](#-distributed-vcs-dvcs)
- [CVCS vs DVCS Comparison](#-cvcs-vs-dvcs-comparison)
- [What is Git?](#-what-is-git)

---

## 💡 What is a Version Control System?

A **Version Control System (VCS)** is software that records changes to files over time, so you can recall specific versions later, compare changes, and collaborate without overwriting each other's work.

Without a VCS, developers resort to manually creating file copies:

```
project/
├── project_v1.zip
├── project_v2.zip
├── project_final.zip
├── project_final_v2.zip
└── project_final_ACTUALLY_FINAL.zip   ← chaos
```

This breaks down quickly — you lose track of what changed, who changed it, and why. A VCS solves all of this systematically.

A VCS lets you:
- Track every change made to every file over time
- Revert files or entire projects back to any previous state
- Compare changes between versions
- See who made a change, when, and why (via commit messages)
- Collaborate with multiple people without conflicts

---

## 🏢 Centralized VCS (CVCS)

In a **Centralized VCS**, there is a **single central server** that holds the entire repository. Developers check out files from this server, make changes, and check them back in.

```
                ┌─────────────────────┐
                │   Central Server    │
                │  (Full Repository)  │
                └──────────┬──────────┘
                           │
          ┌────────────────┼────────────────┐
          │                │                │
    ┌─────▼─────┐    ┌─────▼─────┐    ┌─────▼─────┐
    │  Dev A    │    │  Dev B    │    │  Dev C    │
    │ (checkout)│    │ (checkout)│    │ (checkout)│
    └───────────┘    └───────────┘    └───────────┘
```

**Characteristics:**
- One central server stores all history
- Requires a **constant network connection** to commit, diff, or view history
- If the central server goes down, **nobody can collaborate**
- If the server is lost without backup, **all history is gone**

**Examples:** Subversion (SVN), CVS, Perforce

---

## 🌐 Distributed VCS (DVCS)

In a **Distributed VCS**, every developer has the **full repository — including complete history** — on their local machine. The central server is used for sharing and collaboration, not as a single source of truth.

```
                ┌─────────────────────┐
                │   Remote Server     │
                │  (Shared Repo)      │
                └──────────┬──────────┘
                           │  push / pull
          ┌────────────────┼────────────────┐
          │                │                │
    ┌─────▼─────┐    ┌─────▼─────┐    ┌─────▼─────┐
    │  Dev A    │    │  Dev B    │    │  Dev C    │
    │ Full Repo │    │ Full Repo │    │ Full Repo │
    │ + History │    │ + History │    │ + History │
    └───────────┘    └───────────┘    └───────────┘
```

**Characteristics:**
- Every developer has the **entire repo and full history** locally
- Commit, diff, log, branch — all work **offline**
- Faster operations — most actions don't need the network
- Safer — if the central server is lost, any developer's copy can restore it

**Examples:** Git, Mercurial, Bazaar

---

## ⚖️ CVCS vs DVCS Comparison

| Feature | CVCS (Centralized) | DVCS (Distributed) |
|---------|-------------------|-------------------|
| Repository Location | Single central server | Every developer has full copy |
| Offline Support | ❌ No — network required for most ops | ✅ Yes — all local operations work offline |
| Speed | Slower — network dependency | Faster — commits, diffs, logs are local |
| Fault Tolerance | ❌ Server crash = potential data loss | ✅ Every clone is a full backup |
| Branching | Slow and expensive | Fast and lightweight |
| Examples | SVN, CVS, Perforce | Git, Mercurial |

---

## 🔧 What is Git?

**Git** is the world's most widely used **Distributed Version Control System (DVCS)**.

It was created in **2005 by Linus Torvalds** — the creator of the Linux kernel — because he needed a fast, distributed, and reliable VCS to manage the massive Linux kernel codebase after the team's previous tool became unavailable.

Git became the dominant VCS because of its:

| Quality | What It Means |
|---------|--------------|
| **Speed** | Optimized for large codebases — most operations run locally in milliseconds |
| **Data Integrity** | Every file and commit is checksummed with SHA-1 — corruption is immediately detected |
| **Distributed Nature** | No single point of failure — every clone is a full backup |
| **Efficient Branching** | Creating and merging branches is fast, cheap, and safe |
| **Open Source** | Free to use, massive ecosystem of tooling and hosting platforms |

Today, Git is used by virtually every software team in the world — from solo hobby projects to the Linux kernel with thousands of contributors.

---

<div align="center">

*Part of the [Git & GitHub Zero to Hero](../README.md) course*

</div>
