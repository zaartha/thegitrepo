# Exercise 02 — Resolving Conflicts

## Setup
1. `echo "ENV=production" > config.txt` on `main`, commit
2. Branch `feature-config`, change to `ENV=staging`, commit
3. On `main`, change to `ENV=development`, commit

## Task
4. `git merge feature-config` — conflict!
5. Resolve manually, stage, complete the merge

## Bonus
Try `git merge --abort` before resolving to see how to back out cleanly.
