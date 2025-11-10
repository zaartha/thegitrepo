# Chapter 01 — Git Fundamentals

> **Estimated time:** 3–4 hours &nbsp;|&nbsp; **Difficulty:** Beginner &nbsp;|&nbsp; **Prerequisites:** None

---

## What This Chapter Covers

This chapter builds your mental model of Git from the ground up. Before touching advanced commands, you need to deeply understand *how Git thinks* — the four areas, the staging model, and the commit graph. Everything else in this course builds on these concepts.

---

## Learning Objectives

By the end of this chapter, you will be able to:

- [ ] Explain what Git is and how it differs from GitHub
- [ ] Describe the four areas of Git: Working Directory, Staging Area, Local Repository, Remote Repository
- [ ] Install and verify Git, and configure your identity
- [ ] Initialize a new repository and clone an existing one
- [ ] Use `git status` to understand the state of your working directory at any moment
- [ ] Stage specific files and partial changes using `git add` and `git add -p`
- [ ] Write meaningful commit messages following professional conventions
- [ ] Read `git log` output and navigate commit history
- [ ] Create, switch, and manage branches confidently
- [ ] Perform fast-forward and merge-commit merges
- [ ] Push and pull from a remote repository
- [ ] Set upstream tracking branches
- [ ] Create and push annotated tags for releases
- [ ] Delete local and remote branches safely
- [ ] Cherry-pick specific commits within and across repositories

---

## Files in This Chapter

```
chapter-01/
├── README.md          ← This file
├── lesson.md          ← Full lesson (read this first)
└── exercises/
    ├── 01-setup.md
    ├── 02-first-commit.md
    ├── 03-staging.md
    ├── 04-history.md
    ├── 05-branches.md
    ├── 06-remotes.md
    ├── 07-tags.md
    ├── 08-cherry-pick.md
    └── solutions/
        ├── 01-setup-solution.md
        ├── 02-first-commit-solution.md
        └── ...
```

---

## How to Work Through This Chapter

### Step 1 — Read the lesson

```bash
# Open the main lesson file in your editor
code lesson.md        # VS Code
# or
cat lesson.md | less  # Terminal
```

Work through `lesson.md` from top to bottom. Every command has an explanation — don't skip ahead.

### Step 2 — Do the exercises

Open each exercise file in `exercises/` in order. Do the work in a **separate practice folder** on your machine, not inside this repo.

```bash
# Create a practice folder outside this repo
cd ~
mkdir git-practice
cd git-practice
git init
```

### Step 3 — Check solutions only after trying

Solutions are in `exercises/solutions/`. Look at them *after* attempting the exercise, or if you're truly stuck.

---

## Key Concepts at a Glance

| Concept | One-Line Summary |
|---------|-----------------|
| Working Directory | The files you can see and edit in your folder |
| Staging Area | A draft of your next commit — you choose what goes in |
| Local Repository | The `.git` folder — your full history, stored locally |
| Remote Repository | A copy of your repo hosted elsewhere (e.g. GitHub) |
| Commit | A permanent snapshot of staged changes |
| Branch | A movable pointer to a commit — an independent line of work |
| Tag | A permanent pointer to a commit — typically marks a release |
| Cherry-pick | Copy a specific commit's changes to your current branch |

---

## Commands Introduced in This Chapter

```bash
git --version
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --list
git init
git clone https://github.com/zaartha/thegitrepo.git
git status
git add <file>
git add .
git add -p
git restore --staged <file>
git commit -m "message"
git commit -am "message"
git log
git log --oneline
git log --graph --oneline --all
git show <hash>
git branch
git branch <name>
git switch <name>
git switch -c <name>
git merge <branch>
git remote add origin https://github.com/zaartha/thegitrepo.git
git remote -v
git push -u origin main
git push
git pull
git fetch
git branch --set-upstream-to=origin/main main
git branch -vv
git tag -a v1.0.0 -m "message"
git tag
git show v1.0.0
git push origin v1.0.0
git push origin --tags
git push origin --delete <branch>
git branch -d <name>
git branch -D <name>
git cherry-pick <hash>
git remote add other-repo <url>
git remote remove other-repo
```

---

## Common Mistakes to Watch For

> **Staging everything with `git add .`** without a `.gitignore` in place. You may accidentally commit secrets, build artifacts, or `node_modules`. Always set up `.gitignore` before your first commit.

> **Vague commit messages** like "fix" or "update". A commit message should complete the sentence: *"If applied, this commit will ___."*

> **Confusing `git fetch` and `git pull`.** Fetch downloads changes but doesn't touch your files. Pull downloads *and* merges. When in doubt, fetch first and review.

> **Force-deleting branches with `git branch -D`** without confirming the work is merged or pushed. Unmerged, unpushed commits will be lost.

---

## Ready to Start?

```bash
cat lesson.md
```

When you're done with this chapter, head to Chapter 2:

```bash
git switch chapter-02
```

---

*Chapter 01 of 06 &nbsp;·&nbsp; Next: [Chapter 02 — Branching & Merging →](../chapter-02)*
