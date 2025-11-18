# Solution — Exercise 02: First Commit

```bash
mkdir my-first-repo && cd my-first-repo
git init
echo "# My First Repo" > README.md
git status        # Untracked: README.md
git add README.md
git status        # Staged: README.md
git commit -m "docs: add README"
git log --oneline
# a1b2c3d docs: add README
```
