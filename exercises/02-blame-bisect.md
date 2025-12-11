# Exercise 02 — Blame & Bisect

## Blame
1. `git blame` on any file in this repo
2. Copy a commit hash from the output
3. `git show <hash>` for full context

## Bisect
1. In a repo with several commits, introduce a "bug"
2. `git bisect start`
3. Mark current as bad, an older commit as good
4. Walk through until Git identifies the culprit
5. `git bisect reset`
