# Chapter 1: Git Fundamentals — From Zero to Confident

> **Who this is for:** Developers who are new to Git, or those who've been "getting by" without fully understanding what's happening under the hood. By the end of this chapter, you'll understand not just *what* Git commands do, but *why* they work the way they do.

---

## Table of Contents

1. [Introduction to Git](#1-introduction-to-git)
2. [Verifying Your Installation](#2-verifying-your-installation)
3. [Git Configuration](#3-git-configuration)
4. [Repository Initialization](#4-repository-initialization)
5. [Checking Status](#5-checking-status)
6. [Staging Changes](#6-staging-changes)
7. [Committing Changes](#7-committing-changes)
8. [Viewing History](#8-viewing-history)
9. [Branching Basics](#9-branching-basics)
10. [Merging Branches](#10-merging-branches)
11. [Working with Remote Repositories](#11-working-with-remote-repositories)
12. [Setting an Upstream Branch](#12-setting-an-upstream-branch)
13. [Creating Tags](#13-creating-tags)
14. [Pushing Tags](#14-pushing-tags)
15. [Deleting Remote Branches](#15-deleting-remote-branches)
16. [Deleting Local Branches](#16-deleting-local-branches)
17. [Cherry-Picking Commits](#17-cherry-picking-commits)
18. [Cherry-Picking from Another Repository](#18-cherry-picking-from-another-repository)
19. [Git Cheat Sheet](#19-git-cheat-sheet)

---

## 1. Introduction to Git

### What Is Git?

Git is a **distributed version control system** (DVCS) created by Linus Torvalds in 2005. It tracks changes to files over time so you can recall specific versions later, collaborate with others, and experiment without fear of breaking anything permanently.

Think of Git as a time machine for your code. Every time you make a meaningful change, you take a snapshot. You can always go back to any snapshot, compare snapshots, or branch off into a parallel timeline.

### Why Version Control Matters

Without version control, you've probably done something like this:

```
project/
├── app.js
├── app_backup.js
├── app_final.js
├── app_final_v2.js
└── app_ACTUALLY_FINAL.js
```

This is manual version control — and it breaks down fast. Git solves this by:

- **Tracking every change** with who made it, when, and why
- **Enabling safe experimentation** through branches
- **Facilitating collaboration** without overwriting each other's work
- **Providing a full history** you can search, compare, and revert

### Git vs. GitHub — An Important Distinction

| | Git | GitHub |
|---|---|---|
| **What it is** | A version control tool | A web platform for hosting Git repositories |
| **Runs on** | Your local machine | The cloud |
| **Created by** | Linus Torvalds (2005) | Tom Preston-Werner et al. (2008) |
| **Requires internet?** | No | Yes |

> **Tip:** Git works perfectly fine without GitHub. GitHub (and alternatives like GitLab and Bitbucket) are built *on top of* Git to add collaboration features like pull requests, issue tracking, and CI/CD pipelines.

### The Git Workflow: Four Areas to Understand

Git organizes your work across four distinct areas. Understanding these is the key to understanding every Git command.

```
┌─────────────────────────────────────────────────────────┐
│                    Your Computer                         │
│                                                         │
│  ┌──────────────┐   git add   ┌──────────────┐         │
│  │   Working    │ ──────────► │   Staging    │         │
│  │  Directory   │             │    Area      │         │
│  │              │ ◄────────── │  (Index)     │         │
│  │  (your files)│  git restore│              │         │
│  └──────────────┘             └──────┬───────┘         │
│                                      │ git commit       │
│                                      ▼                  │
│                               ┌──────────────┐         │
│                               │    Local     │         │
│                               │  Repository  │         │
│                               │  (.git dir)  │         │
│                               └──────┬───────┘         │
└──────────────────────────────────────┼─────────────────┘
                                       │ git push
                                       ▼
                               ┌──────────────┐
                               │    Remote    │
                               │  Repository  │
                               │  (GitHub)    │
                               └──────────────┘
```

| Area | Description |
|---|---|
| **Working Directory** | The actual files you see and edit in your project folder |
| **Staging Area (Index)** | A preparation zone — you choose which changes go into your next commit |
| **Local Repository** | The `.git` folder on your machine that stores all history and snapshots |
| **Remote Repository** | A copy of your repository hosted elsewhere (GitHub, GitLab, etc.) |

> **Pro Tip:** The staging area is what makes Git powerful. It lets you craft precise, meaningful commits even when you've made multiple unrelated changes.

---

## 2. Verifying Your Installation

Before writing a single line of code, confirm Git is installed and check which version you have.

### Command

```bash
git --version
```

### Example Output

```
git version 2.47.1
```

If you see a version number, you're good to go. If you get a "command not found" error, visit [git-scm.com](https://git-scm.com) to install Git for your operating system.

> **Tip:** Git 2.28+ introduced helpful defaults like `init.defaultBranch`. Aim to stay reasonably current — anything above 2.30 covers everything in this guide.

---

## 3. Git Configuration

Before you make your first commit, tell Git who you are. This information gets embedded into every commit you make.

### Configure Your Username

```bash
git config --global user.name "Jane Smith"
```

### Configure Your Email

```bash
git config --global user.email "jane@example.com"
```

> **Warning:** Use the same email address associated with your GitHub/GitLab account. This ensures your commits are linked to your profile and contributions are credited correctly.

### Set a Default Branch Name

Modern Git uses `main` as the default branch name (older versions used `master`). Set this globally:

```bash
git config --global init.defaultBranch main
```

### View Your Configuration

```bash
git config --list
```

### Example Output

```
user.name=Jane Smith
user.email=jane@example.com
init.defaultBranch=main
core.editor=vim
...
```

### Global vs. Local Configuration

| Scope | Flag | Location | Applies To |
|---|---|---|---|
| **System** | `--system` | `/etc/gitconfig` | All users on this machine |
| **Global** | `--global` | `~/.gitconfig` | All repos for your user account |
| **Local** | `--local` (default) | `.git/config` | Only the current repository |

Local settings override global, which override system. This lets you use a personal email globally but a work email in a specific project:

```bash
# Inside a work project folder
git config --local user.email "jane@company.com"
```

### 🏋️ Exercise 3

1. Set your name and email globally.
2. Run `git config --list` and verify they appear.
3. Check what value a single key has: `git config user.name`
4. **Bonus:** Open `~/.gitconfig` in a text editor and inspect the raw file format.

---

## 4. Repository Initialization

### Initialize a New Repository

```bash
git init
```

Run this inside an existing project folder (or a new empty folder) to turn it into a Git repository.

```bash
mkdir my-project
cd my-project
git init
```

**Output:**

```
Initialized empty Git repository in /home/jane/my-project/.git/
```

This creates a hidden `.git` directory that stores everything Git needs — history, configuration, branches, and more. **Never manually edit files inside `.git`.**

### Clone an Existing Repository

```bash
git clone <repo-url>
```

Use this to download a copy of a repository that already exists (on GitHub, for example).

```bash
git clone https://github.com/username/my-project.git
```

You can also clone into a specific folder name:

```bash
git clone https://github.com/username/my-project.git custom-folder-name
```

### `git init` vs. `git clone`

| | `git init` | `git clone` |
|---|---|---|
| **Use when** | Starting a brand-new project | Copying an existing repository |
| **Remote set up?** | No — you add it manually | Yes — `origin` is set automatically |
| **Has history?** | No | Yes — full history is downloaded |

> **Pro Tip:** After `git init` on a new project, you'll need to manually add a remote with `git remote add origin <url>` before you can push. `git clone` handles this for you automatically.

### 🏋️ Exercise 4

1. Create a new folder called `git-practice` and initialize a Git repository inside it.
2. Create a file called `README.md` with any content.
3. Confirm the `.git` directory exists: `ls -la`
4. **Bonus:** Clone any public GitHub repository and explore its structure.

---

## 5. Checking Status

```bash
git status
```

`git status` is your best friend. Run it constantly — before staging, after staging, before committing. It shows you exactly what state your working directory and staging area are in.

### Understanding the Output

**Clean working directory:**
```
On branch main
nothing to commit, working tree clean
```

**After creating a new file:**
```
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        README.md

nothing added to commit but untracked files present
```

**After modifying a tracked file:**
```
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
        modified:   app.js
```

**After staging a file:**
```
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   README.md
```

### The Three File States

| State | Meaning |
|---|---|
| **Untracked** | Git sees the file but isn't tracking it yet |
| **Modified** | A tracked file has been changed but not staged |
| **Staged** | The change is in the staging area, ready to commit |

### 🏋️ Exercise 5

1. Inside your `git-practice` repo, run `git status` (should be clean or show untracked files).
2. Create a new file and run `git status` again — note "Untracked files."
3. Stage the file with `git add` and run `git status` — note "Changes to be committed."
4. Make a change to a tracked file and run `git status` — spot the difference between staged and unstaged changes.

---

## 6. Staging Changes

The staging area lets you build your commit piece by piece. You don't have to commit everything at once.

### Stage a Single File

```bash
git add README.md
```

### Stage Multiple Specific Files

```bash
git add app.js styles.css
```

### Stage All Changes in the Current Directory

```bash
git add .
```

### Stage Parts of a File (Interactive)

```bash
git add -p app.js
```

This walks you through each "hunk" of changes interactively, letting you choose exactly which lines to stage. Extremely useful for keeping commits focused.

### Unstage a File

If you staged something by accident:

```bash
git restore --staged README.md
```

> **Warning:** `git add .` stages everything — including files you may not want to commit (like `.env` files with secrets, `node_modules/`, build artifacts). Always use a `.gitignore` file to exclude these. Create one before your first commit.

**Example `.gitignore`:**
```
node_modules/
.env
*.log
dist/
.DS_Store
```

> **Pro Tip:** GitHub maintains a repository of `.gitignore` templates for every language and framework at [github.com/github/gitignore](https://github.com/github/gitignore). Start with one of those.

### 🏋️ Exercise 6

1. Create three files: `index.html`, `styles.css`, `notes.txt`.
2. Stage only `index.html` and `styles.css` (not `notes.txt`).
3. Run `git status` to confirm only those two are staged.
4. Unstage `styles.css` using `git restore --staged styles.css`.
5. Run `git status` again to verify.

---

## 7. Committing Changes

A commit is a permanent snapshot of your staged changes saved to the local repository.

### Basic Commit

```bash
git commit -m "Add homepage layout"
```

The `-m` flag lets you write your commit message inline. Without it, Git opens your default text editor for you to write the message.

### Commit All Tracked Changes (Skip Staging)

```bash
git commit -am "Fix typo in README"
```

The `-a` flag automatically stages all **modified tracked files** before committing. It does **not** include untracked (new) files.

> **Warning:** `git commit -am` is convenient but can lead to imprecise commits. Prefer `git add` + `git commit` for more intentional, focused commits.

### Writing Good Commit Messages

A good commit message answers: **"If applied, this commit will ___."**

**Bad messages:**
```
fix stuff
WIP
asdfgh
update
```

**Good messages:**
```
Add user authentication with JWT
Fix null pointer exception in payment processing
Remove deprecated API endpoints
Update README with setup instructions
```

### The Conventional Commits Standard (Optional but Recommended)

Many teams follow [Conventional Commits](https://www.conventionalcommits.org/) for structured, machine-readable messages:

```
<type>(<scope>): <description>

[optional body]

[optional footer]
```

**Common types:**

| Type | When to Use |
|---|---|
| `feat` | A new feature |
| `fix` | A bug fix |
| `docs` | Documentation changes only |
| `style` | Formatting, no logic change |
| `refactor` | Code change that's neither a fix nor a feature |
| `test` | Adding or fixing tests |
| `chore` | Build process, tooling changes |

**Examples:**
```
feat(auth): add OAuth2 login with Google
fix(cart): prevent duplicate items on rapid click
docs: update API reference for v2 endpoints
```

> **Pro Tip:** Conventional commits unlock automation. Tools like `semantic-release` can automatically bump version numbers and generate changelogs from your commit history.

### 🏋️ Exercise 7

1. Stage `index.html` and commit it with a meaningful message.
2. Make a change to `index.html`, then commit using `git commit -am`.
3. Write three commit messages for imaginary changes using the Conventional Commits format.

---

## 8. Viewing History

### Full Log

```bash
git log
```

Shows commits in reverse chronological order with full details: hash, author, date, and message.

```
commit a3f8c2d1e4b5f6a7b8c9d0e1f2a3b4c5d6e7f8a9
Author: Jane Smith <jane@example.com>
Date:   Mon Jan 15 14:32:10 2025 +0000

    feat(auth): add OAuth2 login with Google
```

### Compact One-Line Log

```bash
git log --oneline
```

```
a3f8c2d feat(auth): add OAuth2 login with Google
b1e2d3f fix(cart): prevent duplicate items
c4f5a6b docs: update API reference
```

### Graph View (Essential for Branches)

```bash
git log --graph --oneline --all
```

```
* a3f8c2d (HEAD -> main) feat(auth): add OAuth2 login
| * b1e2d3f (feature-login) WIP: login form
|/
* c4f5a6b docs: update API reference
* d7e8f9a Initial commit
```

### Filter Logs

```bash
# Commits by a specific author
git log --author="Jane"

# Commits containing a keyword in the message
git log --grep="auth"

# Commits that changed a specific file
git log -- app.js

# Last 5 commits
git log -5
```

### Show What Changed in a Commit

```bash
git show a3f8c2d
```

This displays the commit metadata plus the actual diff (what lines were added/removed).

### 🏋️ Exercise 8

1. Make 3–4 commits in your practice repo with different messages.
2. Run `git log`, `git log --oneline`, and `git log --graph --oneline --all`.
3. Use `git show <hash>` on your most recent commit.
4. **Bonus:** Run `git log --oneline --all --graph --decorate` for a decorated view.

---

## 9. Branching Basics

Branches are Git's killer feature. A branch is an independent line of development — a pointer to a specific commit. Creating a branch is nearly instantaneous and costs almost nothing.

### Visualizing Branches

```
main:    A ── B ── C
                    \
feature:             D ── E
```

When you create `feature` from `main` at commit C, both branches share the history up to C. New commits on `feature` (D, E) don't affect `main`.

### List All Branches

```bash
git branch
```

The `*` marks your current branch.

### Create a New Branch

```bash
git branch feature-login
```

This creates the branch but **does not switch to it**.

### Switch to a Branch

```bash
git switch feature-login
```

Or using the older syntax (still valid):

```bash
git checkout feature-login
```

> **Tip:** `git switch` was introduced in Git 2.23 as a more focused alternative to the multipurpose `git checkout`. Prefer `git switch` for branch operations in modern Git.

### Create and Switch in One Command

```bash
git switch -c feature-login
```

This is the same as `git branch feature-login` followed by `git switch feature-login`.

### See Where You Are

```bash
git branch          # lists branches, shows current with *
git status          # shows current branch at the top
```

### Rename a Branch

```bash
git branch -m old-name new-name
```

### 🏋️ Exercise 9

1. In your practice repo, create a branch called `feature-about-page`.
2. Switch to it and create a file called `about.html`.
3. Commit the new file.
4. Switch back to `main` — notice `about.html` is gone (it's only on the feature branch).
5. Run `git log --graph --oneline --all` to see the branch divergence.

---

## 10. Merging Branches

Once your feature is complete, you merge it back into your main branch.

```bash
# First, switch to the target branch (the one receiving changes)
git switch main

# Then merge the feature branch
git merge feature-login
```

### Fast-Forward Merge

If `main` hasn't moved since you branched off, Git simply moves the `main` pointer forward. No merge commit is created.

```
Before:   main: A ── B
                      \
          feature:     C ── D

After:    main: A ── B ── C ── D   (main pointer moved forward)
```

### Merge Commit

If both branches have diverged (both have new commits), Git creates a new "merge commit" that has two parents.

```
Before:   main: A ── B ── E
                      \
          feature:     C ── D

After:    main: A ── B ── E ── M   (M is the merge commit)
                      \       /
          feature:     C ── D
```

### Merge Conflicts

A conflict happens when the same lines in the same file were changed differently on both branches. Git can't decide which version to keep — it needs your help.

```bash
git merge feature-login
# AUTO-MERGING FAILS:
# CONFLICT (content): Merge conflict in app.js
# Automatic merge failed; fix conflicts and then commit the result.
```

Git marks the conflicting section in the file:

```javascript
<<<<<<< HEAD
const greeting = "Hello, World!";
=======
const greeting = "Hi there!";
>>>>>>> feature-login
```

To resolve: edit the file to keep what you want, remove the conflict markers, then:

```bash
git add app.js
git commit -m "Merge feature-login into main"
```

> **Pro Tip:** Use `git mergetool` to open a visual merge tool. Many editors (VS Code, IntelliJ) also have built-in merge conflict resolution UIs that are far easier than editing raw markers.

---

## 11. Working with Remote Repositories

A remote is a version of your repository hosted elsewhere. The conventional name for your primary remote is `origin`.

### Add a Remote

```bash
git remote add origin https://github.com/username/my-project.git
```

### View Configured Remotes

```bash
git remote -v
```

```
origin  https://github.com/username/my-project.git (fetch)
origin  https://github.com/username/my-project.git (push)
```

### Push to a Remote

```bash
git push origin main
```

This pushes your local `main` branch to the `main` branch on `origin`.

### Pull Changes from a Remote

```bash
git pull origin main
```

`git pull` is a shortcut for two commands: `git fetch` followed by `git merge`.

### Fetch Changes Without Merging

```bash
git fetch origin
```

`git fetch` downloads new commits, branches, and tags from the remote **without modifying your working directory or local branches**. You can then inspect what changed before merging.

### `git pull` vs. `git fetch`

| | `git fetch` | `git pull` |
|---|---|---|
| Downloads remote changes | ✅ | ✅ |
| Updates your local branch | ❌ | ✅ |
| Safe to run anytime | ✅ | Use with care |
| Lets you review before merging | ✅ | ❌ |

> **Pro Tip:** In a team environment, prefer `git fetch` followed by `git log origin/main` to see what changed, then explicitly merge or rebase. This gives you more control and avoids surprise conflicts.

### 🏋️ Exercise 11

1. Create a repository on GitHub (or GitLab).
2. Add it as a remote: `git remote add origin <url>`
3. Push your local commits: `git push origin main`
4. Make a change directly on GitHub (edit a file via the web UI).
5. Run `git fetch origin`, then `git log origin/main --oneline` to see the change.
6. Run `git pull origin main` to bring it down.

---

## 12. Setting an Upstream Branch

An **upstream** (or tracking) branch is the remote branch that your local branch is linked to. Once set, you can use `git push` and `git pull` without specifying the remote and branch name every time.

### Set Upstream While Pushing

```bash
git push -u origin main
```

The `-u` flag (short for `--set-upstream`) pushes and links the local `main` to `origin/main` in one step.

After this, you can simply run:

```bash
git push    # pushes to origin/main automatically
git pull    # pulls from origin/main automatically
```

### Set Upstream for an Existing Branch

If you want to set or change the upstream without pushing:

```bash
git branch --set-upstream-to=origin/main main
```

### Check Tracking Relationships

```bash
git branch -vv
```

```
* main    a3f8c2d [origin/main] feat(auth): add OAuth2 login
  feature b1e2d3f [origin/feature: ahead 2] WIP
```

This shows each local branch, its latest commit, and its upstream (if any). "ahead 2" means you have 2 local commits not yet pushed.

> **Tip:** When you `git clone` a repository, the default branch is automatically set up with an upstream. You only need to manually set it for new branches you create locally.

### 🏋️ Exercise 12

1. Create a new local branch: `git switch -c feature-contact`
2. Make a commit on it.
3. Push with upstream tracking: `git push -u origin feature-contact`
4. Run `git branch -vv` to confirm the tracking relationship.
5. Make another commit and push with just `git push` (no extra arguments needed now).

---

## 13. Creating Tags

Tags mark specific commits as significant — typically software releases. Unlike branches, tags don't move as new commits are added.

### Lightweight Tag

A simple pointer to a commit, no metadata:

```bash
git tag v1.0.0
```

### Annotated Tag (Recommended for Releases)

Stores a tag message, tagger name, email, and date:

```bash
git tag -a v1.0.0 -m "Release version 1.0.0 — initial public release"
```

### Tag a Past Commit

```bash
git tag -a v0.9.0 b1e2d3f -m "Beta release"
```

### List All Tags

```bash
git tag
```

### Search Tags by Pattern

```bash
git tag -l "v1.*"
```

### View Tag Details

```bash
git show v1.0.0
```

For annotated tags, this shows the tagger info, message, and the commit the tag points to.

> **Pro Tip:** Always use annotated tags (`-a`) for releases. They're richer in metadata, they can be signed with GPG for verification, and tools like `git describe` behave better with them.

### 🏋️ Exercise 13

1. Create an annotated tag `v1.0.0` on your current commit.
2. Create a lightweight tag `v1.0.0-beta` on a previous commit (use a hash from `git log --oneline`).
3. Run `git tag` to list both.
4. Run `git show v1.0.0` and `git show v1.0.0-beta` — notice the difference in output.

---

## 14. Pushing Tags

Tags are **not** pushed to the remote by default when you run `git push`. You must push them explicitly.

### Push a Single Tag

```bash
git push origin v1.0.0
```

### Push All Local Tags

```bash
git push origin --tags
```

### Delete a Remote Tag

```bash
git push origin --delete v1.0.0
```

### Release Workflow with Tags

A typical release workflow looks like this:

```bash
# 1. Complete all features and fixes on main
git switch main
git pull origin main

# 2. Tag the release
git tag -a v2.1.0 -m "Release v2.1.0 — add dark mode, fix login bug"

# 3. Push the code and tag
git push origin main
git push origin v2.1.0

# 4. On GitHub, create a Release from this tag (adds release notes, downloadable archives)
```

> **Tip:** Semantic Versioning (SemVer) is the standard format: `MAJOR.MINOR.PATCH`. Increment MAJOR for breaking changes, MINOR for new features, PATCH for bug fixes.

### 🏋️ Exercise 14

1. Push your `v1.0.0` tag to the remote: `git push origin v1.0.0`
2. Push all tags with `git push origin --tags`
3. On GitHub, verify the tag appears under the "Tags" tab.
4. **Bonus:** Create a GitHub Release from the tag via the GitHub UI.

---

## 15. Deleting Remote Branches

Once a feature branch is merged and no longer needed, clean it up on the remote.

```bash
git push origin --delete feature-login
```

### When to Delete Remote Branches

- After a pull request is merged
- After a hotfix is deployed
- To keep the remote repository tidy

> **Warning:** Deleting a remote branch is reversible (with effort) but destructive in practice. Before deleting, confirm the branch has been fully merged. Run `git branch -r --merged main` to list all remote branches already merged into `main`.

### Also Clean Up Stale Remote-Tracking References

After others delete remote branches, your local Git may still show them. Clean up stale references:

```bash
git fetch --prune
```

Or configure Git to prune automatically:

```bash
git config --global fetch.prune true
```

### 🏋️ Exercise 15

1. Create a branch `feature-temp`, push it to the remote.
2. Confirm it appears on GitHub.
3. Delete it from the remote: `git push origin --delete feature-temp`
4. Run `git branch -r` and then `git fetch --prune` to remove the stale reference locally.

---

## 16. Deleting Local Branches

### Safe Delete (Checks for Unmerged Work)

```bash
git branch -d feature-login
```

Git will **refuse** to delete the branch if it contains commits not yet merged into the current branch. This is your safety net.

```
error: The branch 'feature-login' is not fully merged.
If you are sure you want to delete it, run 'git branch -D feature-login'.
```

### Force Delete (No Safety Check)

```bash
git branch -D feature-login
```

This deletes the branch regardless of merge status.

> **Warning:** `git branch -D` permanently discards unmerged commits on that branch. If you haven't pushed those commits anywhere, they will eventually be garbage-collected and lost. Use this only when you're certain you don't need that work.

### Delete Multiple Branches

```bash
git branch -d feature-login feature-signup feature-profile
```

### 🏋️ Exercise 16

1. Create a branch `test-branch` and switch to another branch.
2. Delete it safely: `git branch -d test-branch`
3. Create another branch `unmerged-branch`, make a commit on it, switch away, and try `git branch -d unmerged-branch` — observe the error.
4. Force-delete it with `git branch -D unmerged-branch`.

---

## 17. Cherry-Picking Commits

Cherry-picking lets you copy a specific commit (or commits) from one branch and apply it to another — without merging the entire branch.

### What Cherry-Pick Does

```
Before:
  main:     A ── B ── C
  hotfix:   A ── B ── X ── Y    (X has the fix you need)

After cherry-pick X onto main:
  main:     A ── B ── C ── X'   (X' is a copy of X's changes)
  hotfix:   A ── B ── X ── Y    (unchanged)
```

Note that `X'` is a **new commit** with a different hash, even though it applies the same changes as `X`.

### Cherry-Pick a Single Commit

```bash
# Find the hash of the commit you want
git log --oneline feature-hotfix

# Apply it to your current branch
git cherry-pick a3f8c2d
```

### Cherry-Pick Multiple Commits

```bash
git cherry-pick commit1hash commit2hash
```

### Cherry-Pick a Range of Commits

```bash
# Cherry-picks all commits from (not including) A up to and including B
git cherry-pick A..B
```

### Common Use Cases

- Applying a bug fix from a release branch to `main`
- Pulling a specific feature from a colleague's branch without merging everything
- Recovering useful work from an abandoned branch

### Handling Cherry-Pick Conflicts

If a conflict occurs:

```bash
# Resolve conflicts in the affected files, then:
git add resolved-file.js
git cherry-pick --continue

# Or abort the cherry-pick:
git cherry-pick --abort
```

> **Warning:** Cherry-picking duplicates commits — the same logical change exists in two branches with different hashes. This can complicate future merges. Use it intentionally, not habitually.

---

## 18. Cherry-Picking from Another Repository

Sometimes the commit you need lives in an entirely separate repository. Git makes this possible by temporarily adding that repo as a remote.

### The Full Workflow

**Step 1: Add the other repository as a temporary remote**

```bash
git remote add other-repo https://github.com/colleague/their-project.git
```

**Step 2: Fetch its data (without merging)**

```bash
git fetch other-repo
```

**Step 3: Find the commit you want**

```bash
git log other-repo/main --oneline
```

```
f9e8d7c fix: resolve memory leak in image processing
e5f6g7h feat: add WebP support
...
```

**Step 4: Cherry-pick the commit**

```bash
git cherry-pick f9e8d7c
```

**Step 5: Remove the temporary remote**

```bash
git remote remove other-repo
```

### Real-World Example: Copying a Bug Fix Between Projects

Your company has two related applications: `app-web` and `app-mobile`. A developer on `app-mobile` fixed a critical data validation bug that also affects `app-web`.

```bash
# In the app-web repository:
git remote add app-mobile https://github.com/company/app-mobile.git
git fetch app-mobile

# Find the fix commit
git log app-mobile/main --oneline --grep="data validation"
# Output: 8a7b6c5 fix: prevent XSS via input sanitization

# Apply it
git cherry-pick 8a7b6c5

# Clean up
git remote remove app-mobile

# Push the fix
git push origin main
```

> **Pro Tip:** Always review what a commit does before cherry-picking from an external repository: `git show other-repo/main~0` or `git show <hash>`. You're importing code you may not be fully familiar with.

### 🏋️ Exercise 18

1. Create two separate Git repositories on your machine.
2. Make 3 commits on a branch in repo 1.
3. In repo 2, add repo 1 as a remote and fetch it.
4. Cherry-pick one specific commit from repo 1 into repo 2.
5. Remove the temporary remote and verify your repo 2 history with `git log --oneline`.

---

## 19. Git Cheat Sheet

### Core Workflow

| Task | Command |
|---|---|
| Initialize repository | `git init` |
| Clone repository | `git clone <url>` |
| Check status | `git status` |
| Stage a file | `git add <file>` |
| Stage all changes | `git add .` |
| Commit staged changes | `git commit -m "message"` |
| Commit all tracked changes | `git commit -am "message"` |
| View history | `git log --oneline` |

### Branching

| Task | Command |
|---|---|
| List branches | `git branch` |
| Create branch | `git branch <name>` |
| Switch to branch | `git switch <name>` |
| Create and switch | `git switch -c <name>` |
| Merge branch into current | `git merge <name>` |
| Delete branch (safe) | `git branch -d <name>` |
| Force delete branch | `git branch -D <name>` |

### Remote Operations

| Task | Command |
|---|---|
| Add remote | `git remote add origin <url>` |
| View remotes | `git remote -v` |
| Push with upstream | `git push -u origin <branch>` |
| Push | `git push` |
| Pull | `git pull` |
| Fetch only | `git fetch` |
| Delete remote branch | `git push origin --delete <branch>` |
| Prune stale remotes | `git fetch --prune` |

### Tags

| Task | Command |
|---|---|
| Create annotated tag | `git tag -a v1.0.0 -m "message"` |
| Create lightweight tag | `git tag v1.0.0` |
| List tags | `git tag` |
| Show tag details | `git show v1.0.0` |
| Push a tag | `git push origin v1.0.0` |
| Push all tags | `git push origin --tags` |
| Delete remote tag | `git push origin --delete v1.0.0` |

### Advanced

| Task | Command |
|---|---|
| Cherry-pick a commit | `git cherry-pick <hash>` |
| Set upstream branch | `git branch --set-upstream-to=origin/main main` |
| View tracking branches | `git branch -vv` |
| Add temporary remote | `git remote add temp-remote <url>` |
| Remove remote | `git remote remove <name>` |
| View commit changes | `git show <hash>` |

---

## What's Next?

You've covered the core of Git — from initializing a repo to cherry-picking commits across repositories. In the next chapter, we'll go deeper into:

- **Rebasing** — a cleaner alternative to merge for linear history
- **Stashing** — temporarily shelving work in progress
- **Undoing mistakes** — `git reset`, `git revert`, `git restore` in depth
- **Git workflows** — GitFlow, trunk-based development, and how teams collaborate

> **Final Tip:** The best way to get comfortable with Git is to use it every day. Even for personal projects, practice making small, focused commits with clear messages. Your future self (and your teammates) will thank you.

---

*Chapter 1 complete. Estimated reading time: 45–60 minutes. All commands tested against Git 2.47.*
