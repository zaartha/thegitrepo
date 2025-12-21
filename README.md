# Chapter 05 — Rebasing & History Rewriting

> **Estimated time:** 3–4 hours | **Difficulty:** Intermediate–Advanced | **Prerequisites:** Chapters 01–04

## Learning Objectives

- [ ] Use `git rebase -i` to edit, reorder, squash, and drop commits
- [ ] Squash a branch's commits into one before merging
- [ ] Fix a commit deep in history
- [ ] Use `git commit --fixup` and `--autosquash` together
- [ ] Apply the golden rule: never rebase public history

## Key Commands

```bash
git rebase -i HEAD~4
git rebase -i main
git commit --fixup <hash>
git rebase -i --autosquash main
```

## Ready to Start?

```bash
cat lesson.md
```

*Chapter 05 of 06 · Previous: [Chapter 04](../chapter-04) · Next: [Chapter 06](../chapter-06)*
