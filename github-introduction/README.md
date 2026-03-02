<img src="https://github.com/bhuvan-raj/Git-GitHub-Zero-to-Hero/blob/main/assets/github.png" alt="Banner" />

<div align="center">

![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)
![Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=for-the-badge&logo=github-actions&logoColor=white)
![Docker](https://img.shields.io/badge/GHCR-Container%20Registry-2496ED?style=for-the-badge&logo=docker&logoColor=white)

# Introduction to GitHub

> **Git is the tool. GitHub is the platform built around it — and it does a lot more than just host code.**

</div>

---

## 📋 Table of Contents

- [What is GitHub?](#-what-is-github)
- [GitHub Container Registry (GHCR)](#-github-container-registry-ghcr)
- [GitHub Actions](#-github-actions)
- [GitHub Projects](#-github-projects)
- [GitHub Marketplace](#-github-marketplace)
- [GitHub Codespaces](#-github-codespaces)
- [Other Features](#-other-features)
- [Summary Table](#-summary-table)

---

## 💡 What is GitHub?

**GitHub** is a **cloud-based Git repository hosting platform** that allows developers to store, manage, and collaborate on code using Git. It was the platform that brought Git-based collaboration to the mainstream.

Beyond repository hosting, GitHub has evolved into a full **developer platform** with CI/CD, container registries, project management, security scanning, and cloud development environments — all tightly integrated around your code.

### Core Git hosting features:

- **Repository Management** — Create, clone, fork, and manage repositories
- **Pull Requests (PRs)** — Propose, review, and discuss changes before merging
- **Issues & Discussions** — Bug tracking, feature requests, and community conversations
- **Access Control** — Public or private repos, collaborator permissions, org teams
- **Web Interface + CLI** — Use GitHub via browser, the `gh` CLI tool, or REST/GraphQL APIs

---

## 📦 GitHub Container Registry (GHCR)

**GHCR** is GitHub's built-in **container image hosting service** — like Docker Hub, but integrated directly into the GitHub ecosystem.

It allows developers to **build, store, and distribute Docker and OCI container images** alongside their source code in the same platform.

### Key features:

- Host **public** and **private** container images
- **Integrated authentication** via GitHub Personal Access Tokens or GitHub Actions tokens
- Image tags are **linked to repository commits** for full traceability
- **Fine-grained access control** per user, team, or organization

### Example usage:

```bash
# Tag your local image for GHCR
docker tag myapp ghcr.io/username/myapp:v1.0

# Push to GHCR
docker push ghcr.io/username/myapp:v1.0

# Pull from GHCR
docker pull ghcr.io/username/myapp:v1.0
```

Having code and container images in one platform improves **security, traceability, and CI/CD simplicity** — your pipeline can build an image and push it to GHCR in the same workflow that runs your tests.

---

## ⚡ GitHub Actions

**GitHub Actions** is GitHub's built-in **CI/CD automation platform**. It lets you define automated workflows triggered by repository events — pushing code, opening a PR, merging, or on a schedule.

### How it works:

- Workflows are defined in `.github/workflows/` as **YAML files**
- They run on **GitHub-hosted runners** (Ubuntu, Windows, macOS) or your own **self-hosted runners**
- Triggered by events like `push`, `pull_request`, `schedule`, or `workflow_dispatch`

### What you can automate:

- Build and test your application on every push
- Run linting and code quality checks
- Build and push Docker images to GHCR
- Deploy to cloud providers (AWS, GCP, Azure)
- Send notifications on failures
- Automate dependency updates

### Example workflow — Build a Java app with Maven:

```yaml
name: CI Build

on:
  push:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Set up JDK 17
        uses: actions/setup-java@v3
        with:
          java-version: '17'
          distribution: 'temurin'

      - name: Build with Maven
        run: mvn clean package

      - name: Run tests
        run: mvn test
```

Every push to `main` triggers this workflow automatically — no manual steps needed.

---

## 📊 GitHub Projects

**GitHub Projects** is GitHub's integrated **project management tool** that lets teams organize, plan, and track work directly alongside their codebase.

### Two versions:

**Classic Projects** — Kanban-style boards (similar to Trello). Simple columns like To Do, In Progress, Done.

**Projects (new)** — A more powerful system combining GitHub Issues with a flexible database-style view. Supports custom fields, filters, grouping, and multiple views (Table, Board, Roadmap).

### Features:

- Track work as **GitHub Issues** and **Pull Requests**
- Add custom fields (status, priority, story points, owner)
- Automate transitions — e.g., auto-move an issue to "Done" when its PR is merged
- **Table view, Board view, Roadmap view** — choose the best layout for your team

### Typical use case:

A development team uses GitHub Projects to manage their sprint, assign issues to team members, track progress across features, and link each issue to the PR that resolves it — all within GitHub, no separate tool needed.

---

## 🛒 GitHub Marketplace

**GitHub Marketplace** is a catalog of **third-party tools and GitHub Actions** that extend your development workflow with one-click installation.

### What's available:

- **Ready-made Actions** — reusable CI/CD steps you add to your workflows
- **Security & scanning tools** — vulnerability detection, SAST, secret scanning
- **Code quality** — linters, formatters, coverage tools
- **Project management integrations** — Jira, Linear, Asana
- **Notification tools** — Slack, email, PagerDuty

### Popular tools:

- **Dependabot** — Automatically opens PRs to update outdated dependencies
- **CodeQL** — Deep static security analysis for your codebase
- **SonarCloud** — Code quality and security scanning
- **Snyk** — Dependency vulnerability detection
- **Codecov** — Test coverage reporting and enforcement

All tools integrate natively with your GitHub repository — no complex setup required.

---

## 💻 GitHub Codespaces

**GitHub Codespaces** provides an **instant, cloud-hosted development environment** that runs in your browser or inside VS Code — fully configured and ready to code in seconds.

### The problem it solves:

Setting up a local development environment can take hours — installing the right language runtimes, dependencies, extensions, and tools. With Codespaces, a new team member can be writing code within **60 seconds** of being added to a repository.

### How it works:

- Each Codespace is a **containerized environment** running on GitHub's cloud VMs
- Pre-configured via a `.devcontainer.json` file in your repository
- Includes the repository code, all dependencies, VS Code extensions, and terminal access
- Environments are **persistent** — your Codespace saves state between sessions

### How to open a Codespace:

1. On any GitHub repository, click **Code → Codespaces → New Codespace**
2. GitHub launches a cloud VS Code session with the repository loaded
3. Start coding, committing, and pushing — all from the browser

### Features:

- **Port forwarding** — expose local ports to preview web apps
- **Prebuilds** — pre-warm environments for instant startup
- **Multiple machine types** — 2, 4, 8, 16, 32 vCPU options

---

## 🧮 Other Features

| Feature | Description |
|---------|-------------|
| **GitHub Pages** | Host static websites directly from a repository — free for public repos |
| **GitHub Packages** | Host language packages (npm, Maven, NuGet, RubyGems, PyPI) alongside code |
| **Discussions** | Community Q&A and long-form conversation boards within a repository |
| **Dependabot** | Automated dependency update PRs and security vulnerability alerts |
| **GitHub Copilot** | AI coding assistant by GitHub + OpenAI — suggests code inline as you type |
| **Secret Scanning** | Detects accidentally committed credentials and API keys |
| **Code Review Tools** | Inline PR comments, review requests, required approvals before merge |

---

## 📌 Summary Table

| GitHub Service | Purpose | Example Use Case |
|---------------|---------|-----------------|
| **Repository Hosting** | Store and manage source code | Team collaboration with Git |
| **GHCR** | Container image registry | Store and share Docker images securely |
| **GitHub Actions** | CI/CD automation | Build, test, and deploy on every push |
| **GitHub Projects** | Project management | Sprint planning and task tracking |
| **Marketplace** | Extensions and integrations | Add security scanning or Slack alerts |
| **Codespaces** | Cloud development environments | Develop instantly from any browser |

---

<div align="center">

*Part of the [Git & GitHub Zero to Hero](../README.md) course*

</div>
