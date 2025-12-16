# Chapter 04: Undoing Mistakes

## 1. Amend the Last Commit

```bash
git commit --amend -m "corrected message"   # fix message

git add forgotten.js
git commit --amend --no-edit               # add forgotten file
```

> **Warning:** `--amend` rewrites the hash. Never amend a pushed commit.

## 2. Git Reset

### Soft — keep staged
```bash
git reset --soft HEAD~1
```

### Mixed — keep in working directory (default)
```bash
git reset HEAD~1
```

### Hard — discard everything
```bash
git reset --hard HEAD~1
```

> **Warning:** `--hard` can lose work permanently. Check `git reflog` immediately if run by accident.

## 3. Git Revert

Creates an "undo" commit. Safe on shared branches — nothing is rewritten.

```bash
git revert a3f8c2d

git revert --no-commit a3f8c2d   # stage the undo, review before committing
```

## 4. Restore a File

```bash
git restore app.js                         # restore to last commit
git restore --source=a3f8c2d app.js        # restore to specific commit
```

## 5. Full Decision Table

| Situation | Command |
|-----------|---------|
| Fix last commit message (not pushed) | `git commit --amend` |
| Undo last commit, keep staged | `git reset --soft HEAD~1` |
| Undo last commit, keep in WD | `git reset HEAD~1` |
| Undo last commit, discard all | `git reset --hard HEAD~1` |
| Undo a pushed commit safely | `git revert <hash>` |
| Restore one file | `git restore --source=<hash> <file>` |
| Recover anything | `git reflog` |
