# Setup Guide

Everything you need before starting Chapter 01.

---

## 1. Install Git

| OS | Instructions |
|----|-------------|
| **macOS** | Run `xcode-select --install` in Terminal, or install via [Homebrew](https://brew.sh): `brew install git` |
| **Windows** | Download from [git-scm.com](https://git-scm.com/download/win). During install, choose "Git from the command line and also from 3rd-party software" and use the default settings. |
| **Linux (Debian/Ubuntu)** | `sudo apt update && sudo apt install git` |
| **Linux (Fedora)** | `sudo dnf install git` |

Verify the installation:

```bash
git --version
# Expected: git version 2.x.x
```

Aim for Git 2.28 or newer. All commands in this course are tested against Git 2.47.

---

## 2. Configure Your Identity

Every commit you make is stamped with your name and email. Set these once globally:

```bash
git config --global user.name "Your Full Name"
git config --global user.email "you@example.com"
```

Set the default branch name to `main` (modern standard):

```bash
git config --global init.defaultBranch main
```

Set your preferred editor for commit messages (choose one):

```bash
git config --global core.editor "code --wait"    # VS Code
git config --global core.editor "nano"           # Nano (beginner-friendly)
git config --global core.editor "vim"            # Vim
```

Verify everything looks correct:

```bash
git config --list
```

---

## 3. Set Up SSH Authentication (Recommended)

SSH keys let you push and pull from GitHub without entering your password every time.

### Generate a key

```bash
ssh-keygen -t ed25519 -C "you@example.com"
# Press Enter to accept the default file location
# Optionally set a passphrase for extra security
```

### Add the key to your SSH agent

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

### Add the public key to GitHub

```bash
# Copy your public key to clipboard
cat ~/.ssh/id_ed25519.pub
```

Then go to **GitHub → Settings → SSH and GPG keys → New SSH key** and paste it.

### Test the connection

```bash
ssh -T git@github.com
# Expected: Hi username! You've successfully authenticated...
```

---

## 4. Choose a Text Editor

You'll spend a lot of time reading Markdown lesson files. Any editor works, but these have excellent Git integration:

- **[VS Code](https://code.visualstudio.com)** — Recommended. Built-in Git panel, diff viewer, merge conflict UI.
- **[JetBrains IDEs](https://www.jetbrains.com/idea/)** — Excellent Git tooling for Java/Python/etc. projects.
- **Vim/Neovim** — Powerful if you already know it; steep learning curve otherwise.

---

## 5. Clone This Repository

```bash
git clone https://github.com/zaartha/thegitrepo.git
cd thegitrepo
```

Confirm you can see all chapter branches:

```bash
git branch -r
```

You should see `origin/chapter-01`, `origin/chapter-02`, etc.

---

## You're Ready

Switch to Chapter 01 and begin:

```bash
git switch chapter-01
cat README.md
```
