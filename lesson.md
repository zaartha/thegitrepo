# Chapter 05: Rebasing & History Rewriting

## 1. Interactive Rebase

```bash
git rebase -i HEAD~4
```

Editor shows oldest-first:
```
pick a1b2c3d feat: add login form
pick b2c3d4e fix: typo in label
pick c3d4e5f fix: another typo
pick d4e5f6a feat: add logout button
```

### Actions

| Action | Effect |
|--------|--------|
| `pick` | Keep as-is |
| `reword` | Keep, edit message |
| `edit` | Pause to amend |
| `squash` | Combine with previous, edit message |
| `fixup` | Combine with previous, discard message |
| `drop` | Delete entirely |

### Squash typo fixes into the feature:

```
pick a1b2c3d feat: add login form
fixup b2c3d4e fix: typo in label
fixup c3d4e5f fix: another typo
pick d4e5f6a feat: add logout button
```

Result: clean two-commit history.

## 2. The `--fixup` Workflow

```bash
git add .
git commit --fixup a1b2c3d        # marks this as a fix for a1b2c3d

git rebase -i --autosquash main   # Git auto-orders and marks fixups
```

## 3. The Golden Rule

> **Never rebase commits that exist on a remote branch others have pulled.**

```
Safe:   your local feature branch (not yet pushed)
Never:  main, develop, any shared branch
```

## 4. Squash Merge on GitHub

When merging a PR, choose **"Squash and merge"** — combines all PR commits into one on `main`. No interactive rebase needed.
