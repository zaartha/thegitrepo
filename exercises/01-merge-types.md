# Exercise 01 — Merge Types

## Part A: Fast-Forward
1. Create `feature-ff`, add a commit
2. Merge into `main` — note "Fast-forward" in output
3. Check `git log --oneline --graph` — no merge commit

## Part B: Three-Way
1. Create `feature-3way`, add a commit
2. On `main`, add a different commit (branches diverge)
3. Merge `feature-3way` — Git creates a merge commit
4. Compare graphs between Part A and B
