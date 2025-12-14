# Chapter 04 — Undoing Mistakes

> **Estimated time:** 2–3 hours | **Difficulty:** Intermediate | **Prerequisites:** Chapters 01–03

## Learning Objectives

- [ ] Amend the most recent commit
- [ ] Use `git reset` in soft, mixed, and hard modes
- [ ] Use `git revert` to safely undo on a shared branch
- [ ] Restore a file to a previous version
- [ ] Recover deleted branches using `git reflog`
- [ ] Know when to use reset vs. revert

## Decision Guide

```
Pushed to shared branch?
├── YES → git revert  (safe, adds an undo commit)
└── NO  → git reset
           ├── Keep staged?    --soft
           ├── Keep in WD?     --mixed
           └── Discard all?    --hard ⚠️
```

## Ready to Start?

```bash
cat lesson.md
```

*Chapter 04 of 06 · Previous: [Chapter 03](../chapter-03) · Next: [Chapter 05](../chapter-05)*
