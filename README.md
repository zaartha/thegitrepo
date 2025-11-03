# 🧠 Git Mastery — A Practical Course for Developers

> Learn Git the way professionals use it — hands-on, example-driven, and branch by branch.

---

## What You'll Learn

By completing this course you will be able to:

- Confidently use Git in real-world projects and team environments
- Understand *why* Git works the way it does, not just *what* commands to type
- Write clean commit histories that communicate intent
- Work with branches, remotes, tags, and advanced workflows
- Recover from mistakes without panic

---

## How This Course Is Organized

Each chapter lives on its own branch. You navigate the course using Git itself — which means you're practicing the very skills you're learning.

```
main              ← You are here (course overview + setup)
├── chapter-01    ← Git Fundamentals
├── chapter-02    ← Branching & Merging (deep dive)
├── chapter-03    ← Remotes & Collaboration
├── chapter-04    ← Undoing Mistakes
├── chapter-05    ← Rebasing & History Rewriting
└── chapter-06    ← Git Workflows for Teams
```

Each chapter branch contains:

```
├── README.md       ← Chapter overview and learning objectives
├── lesson.md       ← Full lesson content
├── exercises/      ← Hands-on tasks
│   └── solutions/  ← Reference solutions
└── assets/         ← Diagrams and supporting files
```

---

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/zaartha/thegitrepo.git
cd thegitrepo
```

### 2. See all available chapters

```bash
git branch -r
```

### 3. Start with Chapter 1

```bash
git switch chapter-01
```

### 4. Read the chapter README

```bash
cat README.md
```

Then open `lesson.md` in your editor and follow along.

---

## Navigating Between Chapters

```bash
# Move to any chapter
git switch chapter-02

# Return to this overview at any time
git switch main

# See all chapters at a glance
git log --all --oneline --graph
```

---

## Course Chapters

| Chapter | Branch | Topic | Prerequisites |
|---------|--------|-------|---------------|
| 01 | `chapter-01` | Git Fundamentals | None |
| 02 | `chapter-02` | Branching & Merging | Chapter 01 |
| 03 | `chapter-03` | Remotes & Collaboration | Chapter 02 |
| 04 | `chapter-04` | Undoing Mistakes | Chapter 03 |
| 05 | `chapter-05` | Rebasing & History Rewriting | Chapter 04 |
| 06 | `chapter-06` | Git Workflows for Teams | Chapter 05 |

---

## Before You Begin

Make sure you have Git installed and configured. Read `SETUP.md` before starting Chapter 01:

```bash
git switch main
cat SETUP.md
```

---

## How to Do the Exercises

Each chapter has an `exercises/` folder with numbered task files. Work through them in order. If you get stuck, solutions are in `exercises/solutions/` — but try first.

We recommend:

1. Read through the full `lesson.md` once before attempting exercises
2. Work in a separate practice folder, not inside this repo itself
3. Re-read the relevant section if a concept isn't clicking — that's normal

---

## Tips for Getting the Most Out of This Course

- **Type every command yourself.** Copying and pasting skips the muscle memory.
- **Break things on purpose.** Git is very hard to permanently damage. Experiment freely.
- **Read error messages carefully.** Git's error output is unusually helpful and often tells you exactly what to do.
- **Use `git status` obsessively.** Before and after every command until it becomes second nature.

---

*This course is maintained at [github.com/zaartha/thegitrepo](https://github.com/zaartha/thegitrepo). Found a typo or error? Open an issue or submit a pull request.*
