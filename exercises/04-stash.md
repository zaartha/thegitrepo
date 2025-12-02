# Exercise 04 — Git Stash

## Scenario
You're mid-edit when an urgent bug is reported on `main`.

1. Edit a file without committing
2. `git stash push -m "WIP: in-progress feature"`
3. `git status` — confirm clean working tree
4. Fix the bug on `main`, commit
5. Switch back to your feature branch
6. `git stash pop`
7. Confirm your in-progress work is restored
