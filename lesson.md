# Chapter 03: Remotes & Collaboration

## 1. Managing Multiple Remotes

```bash
git remote -v
git remote add upstream https://github.com/original/project.git
git remote rename origin old-origin
git remote remove upstream
```

### Keeping a Fork in Sync

```bash
git fetch upstream
git switch main
git merge upstream/main
git push origin main
```

## 2. Fetch Strategies

```bash
git fetch origin
git log origin/main --oneline --not main   # see what's new
git diff main origin/main                  # compare
git merge origin/main                      # merge deliberately
```

### Prune Stale References

```bash
git fetch --prune
git config --global fetch.prune true
```

## 3. Fork-Based Workflow

```
1. Fork on GitHub
2. Clone your fork
3. Add original as "upstream"
4. Create a feature branch
5. Push to your fork
6. Open a Pull Request
```

```bash
git clone https://github.com/zaartha/project.git
cd project
git remote add upstream https://github.com/original/project.git
git switch -c fix/button-alignment
git push -u origin fix/button-alignment
```

## 4. Pull Requests

Good PR checklist:
- Clear title matching branch/commit naming
- Description: what changed, why, how to test
- Small (< 400 lines) — reviewed faster
- CI passing before requesting review

Review a PR locally:
```bash
git fetch origin pull/42/head:pr-42
git switch pr-42
```

## 5. Git Blame

```bash
git blame app.js
# a3f8c2d (zaartha 2025-11-12) const router = require('express').Router();

git show a3f8c2d   # see full context
```

> **Tip:** Blame isn't for finger-pointing — it's for understanding when and why a line was written.

## 6. Git Bisect

Binary search to find the commit that introduced a bug.

```bash
git bisect start
git bisect bad                  # current is broken
git bisect good v1.0.0          # this was known good

# Test at each step, then:
git bisect bad   # or: git bisect good

git bisect reset                # restore when done
```

Automate with tests:
```bash
git bisect run npm test
```
