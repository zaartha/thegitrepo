# Solution — Exercise 01: Setup

```bash
git --version
# git version 2.47.1

git config --global user.name "Jane Smith"
git config --global user.email "jane@example.com"
git config --global init.defaultBranch main
git config --list
git config user.name
# Jane Smith
```
**Note:** `--global` writes to `~/.gitconfig`. Use `--local` to override per-project.
