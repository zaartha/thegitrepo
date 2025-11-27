# Chapter 02: Branching & Merging — Deep Dive

## 1. How Git Stores Branches

A branch is a file in `.git/refs/heads/` containing a commit hash. Creating one is instantaneous.

```bash
cat .git/refs/heads/main
# a3f8c2d1e4b5f6a7b8c9d0e1f2a3b4c5d6e7f8a9
```

**HEAD** points to your current branch:
```bash
cat .git/HEAD
# ref: refs/heads/main
```

## 2. Fast-Forward Merge

When `main` hasn't moved since branching, Git just moves the pointer forward.

```
Before:   main: A ── B
                      \
          feature:     C ── D

After:    main: A ── B ── C ── D
```

```bash
git switch main
git merge feature-login           # fast-forward
git merge --no-ff feature-login   # force a merge commit
```

## 3. Three-Way Merge

When both branches have diverged, Git creates a merge commit with two parents.

```
Before:   main: A ── B ── E
                      \
          feature:     C ── D

After:    main: A ── B ── E ── M
                      \       /
          feature:     C ── D
```

## 4. Resolving Merge Conflicts

```bash
git merge feature-login
# CONFLICT (content): Merge conflict in app.js
```

Conflict markers:
```
<<<<<<< HEAD
const API_URL = "https://api.production.com";
=======
const API_URL = "https://api.staging.com";
>>>>>>> feature-login
```

Resolve, then:
```bash
git add app.js
git commit -m "merge: resolve API_URL conflict"
# Or abort:
git merge --abort
```

## 5. Git Rebase

Replays your branch's commits on top of another branch.

```
Before:   main: A ── B ── E
                      \
          feature:     C ── D

After rebase:   main: A ── B ── E
                               \
                feature:        C' ── D'
```

```bash
git switch feature-login
git rebase main
```

> **Warning:** Never rebase commits already pushed to a shared branch.

## 6. Merge vs. Rebase

| | Merge | Rebase |
|---|---|---|
| History | Preserves branching | Linear |
| Merge commit | Yes (three-way) | No |
| Safe on shared branches | ✅ | ❌ Local only |

## 7. Git Stash

```bash
git stash                              # shelve changes
git stash push -m "WIP: login form"   # with label
git stash list                         # see all stashes
git stash pop                          # apply and drop latest
git stash apply stash@{1}             # apply specific stash
```

## 8. Git Reflog

```bash
git reflog
# a3f8c2d HEAD@{0}: commit: feat: dark mode
# b1e2d3f HEAD@{1}: rebase: finish

# Recover dropped commit:
git switch -c recovered a3f8c2d
```

> **Pro Tip:** Before panicking about lost work, always check `git reflog` first.
