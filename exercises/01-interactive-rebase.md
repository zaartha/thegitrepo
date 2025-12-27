# Exercise 01 — Interactive Rebase

## Setup
Make 4 commits on a feature branch:
- `feat: add login form`
- `fix: typo in button label`
- `fix: another typo`
- `feat: add logout button`

## Tasks

1. `git rebase -i HEAD~4`
2. Change both `fix:` lines to `fixup`
3. Save and close — Git replays commits
4. `git log --oneline` — should show 2 commits

## Bonus
1. Make a commit, then `git commit --fixup <hash>`
2. `git rebase -i --autosquash main` — observe auto-ordering
