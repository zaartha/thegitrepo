# Exercise 03 — Rebase

1. Create a feature branch, make 2 commits
2. On `main`, make 1 commit (branches diverge)
3. `git switch feature && git rebase main`
4. Compare `git log --oneline --graph --all` before and after
5. Merge to `main` — should be fast-forward now

**Reflection:** How does the graph differ from a three-way merge?
