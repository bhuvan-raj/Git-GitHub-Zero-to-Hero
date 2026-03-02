<img src="https://github.com/bhuvan-raj/Git-GitHub-Zero-to-Hero/blob/main/assets/git.png" alt="Banner" />

<div align="center">

![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![macOS](https://img.shields.io/badge/macOS-000000?style=for-the-badge&logo=apple&logoColor=white)
![Windows](https://img.shields.io/badge/Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white)

# Git Installation & Setup

> **Get Git running on your machine and configured with your identity in under 5 minutes.**

</div>

---

## 📋 Table of Contents

- [Installation](#-installation)
- [First-Time Configuration](#-first-time-configuration)
- [Verify Your Setup](#-verify-your-setup)
- [Config Scope Levels](#-config-scope-levels)
- [Useful Config Extras](#-useful-config-extras)

---

## 💾 Installation

### Ubuntu / Debian

```bash
sudo apt update
sudo apt install git -y
```

### CentOS / Fedora / RHEL

```bash
sudo dnf install git -y
```

### macOS

```bash
brew install git
```

> If Homebrew is not installed, run:
> `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`

### Windows

Download and install **Git for Windows** from [git-scm.com](https://git-scm.com/download/win).

During installation, choose:
- **Default editor** — VS Code or Notepad++ recommended over Vim
- **Default branch name** — select `main`
- **Line ending conversions** — `Checkout Windows-style, commit Unix-style` (recommended)

---

## ⚙️ First-Time Configuration

After installing Git, set your **identity**. Every commit you make is stamped with this name and email — this is how your contributions are attributed in team projects and on GitHub.

```bash
git config --global user.name "Bubu"
git config --global user.email "bubu@example.com"
```

Set the default branch name to `main` (modern standard — replaces the old `master` default):

```bash
git config --global init.defaultBranch main
```

Set your preferred text editor (used when writing commit messages):

```bash
# VS Code (recommended)
git config --global core.editor "code --wait"

# Nano (beginner friendly)
git config --global core.editor "nano"

# Vim
git config --global core.editor "vim"
```

---

## ✅ Verify Your Setup

```bash
# Check Git version
git --version
# git version 2.x.x

# View all config values
git config --list

# Check specific values
git config user.name
git config user.email
```

Expected output of `git config --list`:

```
user.name=Bubu
user.email=bubu@example.com
core.editor=code --wait
init.defaultbranch=main
```

---

## 🔒 Config Scope Levels

Git has three levels of configuration — each level overrides the one above it:

| Scope | Flag | Applies To | File Location |
|-------|------|-----------|--------------|
| System | `--system` | All users on the machine | `/etc/gitconfig` |
| Global | `--global` | Your user account only | `~/.gitconfig` |
| Local | `--local` | Current repository only | `.git/config` |

```bash
# Override global email for just one specific project
git config --local user.email "work@company.com"
```

---

## 🔧 Useful Config Extras

### Open the global config file in your editor

```bash
git config --global --edit
```

### Add handy aliases to save typing

```bash
git config --global alias.st status
git config --global alias.lg "log --oneline --graph --decorate --all"
git config --global alias.cm "commit -m"
```

Now `git st` = `git status` and `git lg` shows a visual branch graph.

### Fix line endings for cross-platform teams

```bash
# macOS / Linux
git config --global core.autocrlf input

# Windows
git config --global core.autocrlf true
```

This prevents unnecessary line-ending differences between Windows and Unix developers on the same team.

---

<div align="center">

*Part of the [Git & GitHub Zero to Hero](../README.md) course*

</div>
