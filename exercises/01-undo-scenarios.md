# Exercise 01 — Undo Scenarios

## Scenario A — Amend
1. Commit with a typo in the message
2. `git commit --amend -m "corrected message"`
3. `git log --oneline` — verify

## Scenario B — Soft Reset
1. Make 2 commits
2. `git reset --soft HEAD~1`
3. Confirm changes are still staged: `git status`

## Scenario C — Hard Reset
1. Make a commit you want to discard
2. `git reset --hard HEAD~1`
3. Confirm file changes are gone

## Scenario D — Revert
1. Make a commit and push it
2. `git revert <hash>`
3. Confirm a new "Revert" commit appears — original still in history
