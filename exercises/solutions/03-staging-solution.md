# Solution — Exercise 03: Staging

```bash
touch index.html styles.css notes.txt
git add index.html styles.css
git status
# Staged:    index.html, styles.css
# Untracked: notes.txt

git restore --staged styles.css
git status
# Staged:    index.html
# Untracked: notes.txt, styles.css
```
**Key point:** `git restore --staged` unstages without losing edits.
