<img src="https://github.com/bhuvan-raj/Git-GitHub-Zero-to-Hero/blob/main/assets/github.png" alt="Banner" />

<div align="center">

![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)
![SSH](https://img.shields.io/badge/SSH-Secure-4EAA25?style=for-the-badge&logo=gnu-bash&logoColor=white)
![Token](https://img.shields.io/badge/PAT-Token%20Auth-orange?style=for-the-badge)

# GitHub Authentication

> **Connect your local Git to GitHub securely — using a Personal Access Token or SSH key.**

</div>

---

## 📋 Table of Contents

- [Why Authentication is Needed](#-why-authentication-is-needed)
- [Authentication Methods Overview](#-authentication-methods-overview)
- [Method 1 — Personal Access Token (PAT)](#-method-1--personal-access-token-pat)
- [Method 2 — SSH Keys](#-method-2--ssh-keys)
- [PAT vs SSH Comparison](#-pat-vs-ssh-comparison)
- [Verify Your Connection](#-verify-your-connection)

---

## 💡 Why Authentication is Needed

When you run `git push`, `git pull`, or `git clone` against a **private** or write-enabled GitHub repository, GitHub must verify who you are before allowing the operation.

GitHub supports two primary authentication methods for local Git:

- **HTTPS + Personal Access Token (PAT)** — use a token as your password
- **SSH Keys** — use a public/private key pair for passwordless authentication

> ⚠️ GitHub removed support for basic username/password authentication in August 2021. You must use either a PAT or SSH — never your GitHub account password.

---

## 🔑 Authentication Methods Overview

| Method | How It Works | Best For |
|--------|-------------|---------|
| **HTTPS + PAT** | Token passed as password in HTTPS URLs | Quick setup, works everywhere |
| **SSH Keys** | Public key on GitHub, private key on your machine | Most secure, no token management, recommended for daily use |
| **GitHub CLI (`gh auth`)** | Browser-based OAuth flow | Interactive login from terminal |

---

## 🪙 Method 1 — Personal Access Token (PAT)

A **Personal Access Token** acts as a password replacement for HTTPS Git operations and GitHub API calls. It can be created with specific scopes and revoked at any time.

### Step 1 — Generate a PAT on GitHub

1. Go to GitHub → **Profile → Settings → Developer Settings → Personal Access Tokens → Tokens (classic)**
2. Click **Generate new token (classic)**
3. Configure:

| Field | Value |
|-------|-------|
| Note | `Git Push Token` (or any descriptive name) |
| Expiration | 90 days (recommended — rotate regularly) |
| Scopes | ✅ `repo` — full repository access |
| | ✅ `workflow` — if using GitHub Actions |

4. Click **Generate token**
5. **Copy the token immediately** — GitHub will never show it again after you leave the page

---

### Step 2 — Use the PAT for Git Operations

#### Option A — Enter when prompted (simplest)

Add your remote and push. Git will prompt for credentials:

```bash
git remote add origin https://github.com/your-username/your-repo.git
git push -u origin main
```

```
Username: your_github_username
Password: <paste your PAT here — not your GitHub password>
```

#### Option B — Store PAT so you are not prompted every time

```bash
# Store credentials permanently on disk
git config --global credential.helper store

# Next time you enter your PAT, Git saves it in ~/.git-credentials
```

Contents of `~/.git-credentials` after saving:

```
https://username:YOUR_TOKEN@github.com
```

For a more secure temporary cache (15 minutes by default):

```bash
git config --global credential.helper cache
```

#### Option C — Embed PAT in remote URL (quick testing only)

```bash
git remote add origin https://your-username:YOUR_PAT@github.com/your-username/repo.git
```

> ⚠️ This embeds your token in plain text in `.git/config` and shell history. Only use this for quick local tests — never on shared systems.

---

### Step 3 — Verify PAT Works

```bash
git push -u origin main
```

Successful output:

```
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Writing objects: 100% (5/5) 423 bytes, done.
To https://github.com/your-username/repo.git
 * [new branch]      main -> main
```

---

## 🔐 Method 2 — SSH Keys

SSH authentication uses a **public/private key pair**. Your private key stays on your machine and is never shared. You add your public key to GitHub — and from then on, Git authenticates you automatically without any token or password.

### Step 1 — Generate an SSH key pair

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

When prompted:
- **File location** — press Enter to accept the default (`~/.ssh/id_ed25519`)
- **Passphrase** — add one for extra security, or press Enter for no passphrase

This creates two files:

```
~/.ssh/id_ed25519        ← PRIVATE key — never share this
~/.ssh/id_ed25519.pub    ← PUBLIC key — this goes on GitHub
```

### Step 2 — Start the SSH agent and add your key

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

### Step 3 — Copy your public key

```bash
cat ~/.ssh/id_ed25519.pub
```

Copy the entire output — it looks like:

```
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAA... your_email@example.com
```

### Step 4 — Add the public key to GitHub

1. Go to GitHub → **Profile → Settings → SSH and GPG keys → New SSH key**
2. Configure:

| Field | Value |
|-------|-------|
| Title | `My Laptop` (or any descriptive label) |
| Key type | Authentication Key |
| Key | Paste your public key content |

3. Click **Add SSH key**

### Step 5 — Use SSH remote URL

When cloning or adding a remote, use the **SSH URL** instead of HTTPS:

```bash
# Clone using SSH
git clone git@github.com:your-username/your-repo.git

# Or update an existing remote to use SSH
git remote set-url origin git@github.com:your-username/your-repo.git
```

SSH URLs follow the format: `git@github.com:username/repo.git`

### Step 6 — Test SSH connection to GitHub

```bash
ssh -T git@github.com
```

Expected response:

```
Hi your-username! You've successfully authenticated, but GitHub does not provide shell access.
```

From this point, all `git push` and `git pull` operations happen without any password or token prompt.

---

## ⚖️ PAT vs SSH Comparison

| Feature | PAT (HTTPS) | SSH Key |
|---------|------------|---------|
| Setup complexity | Simple | Moderate (key generation + upload) |
| Prompted for credentials | Yes (unless stored) | ❌ Never — fully automatic |
| Token expiry | Yes — must rotate regularly | No expiry unless revoked |
| Security | Good — can be scoped and revoked | Excellent — private key never leaves machine |
| Works behind corporate proxies | ✅ Yes — HTTPS is always allowed | Sometimes blocked |
| Recommended for daily use | ✓ Acceptable | ✅ Preferred |

---

## ✅ Verify Your Connection

### Check your configured remote

```bash
git remote -v
```

### Push to verify authentication works

```bash
git push -u origin main
```

### List credentials stored (PAT method)

```bash
cat ~/.git-credentials
```

### Check SSH key is loaded (SSH method)

```bash
ssh-add -l
```

---

<div align="center">

*Part of the [Git & GitHub Zero to Hero](../README.md) course*

</div>
