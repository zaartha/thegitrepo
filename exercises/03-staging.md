# Exercise 03 — Staging & the Index

## Goal
Practice staging specific files.

## Tasks

1. `touch index.html styles.css notes.txt`
2. Stage only `index.html` and `styles.css`
3. Confirm with `git status` — `notes.txt` should be untracked
4. Unstage `styles.css`: `git restore --staged styles.css`
5. Verify with `git status`
6. **Bonus:** Try `git add -p` on a file with multiple edits
