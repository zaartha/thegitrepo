# Chapter 06: Git Workflows for Teams

## 1. GitFlow

```
main       ← production only, tagged releases
develop    ← integration branch

feature/*  ← from develop → merge back to develop
release/*  ← from develop → merge to main AND develop
hotfix/*   ← from main    → merge to main AND develop
```

**Use when:** versioned software, formal QA cycles, multiple live versions.
**Avoid when:** you deploy multiple times per day.

## 2. Trunk-Based Development

Everyone commits to `main` at least daily. Feature branches live hours, not weeks.

```
main: ── A ── B ── C ── D ── E ──►  (continuous deployment)
```

Enabling techniques:
- **Feature flags** — deploy unfinished code, enable when ready
- **Branch by abstraction** — new implementation alongside old
- **Comprehensive CI** — every commit triggers full test suite

**Use when:** high-trust team, strong CI, continuous deployment.

## 3. GitHub Flow

```
1. Branch from main
2. Commit and push
3. Open a Pull Request
4. Review + CI passes
5. Merge to main
6. Deploy
```

No `develop`. No release branches. Simple and fast.

## 4. Conventional Commits + Automation

```bash
npx semantic-release    # auto version + GitHub release + publish
npx standard-version    # auto version + CHANGELOG.md
```

Commit → version bump:
- `fix:` → patch (1.0.0 → 1.0.1)
- `feat:` → minor (1.0.0 → 1.1.0)
- `feat!:` / `BREAKING CHANGE:` → major (1.0.0 → 2.0.0)

## 5. Git Hooks with Husky

```bash
npm install --save-dev @commitlint/cli @commitlint/config-conventional husky
npx husky add .husky/commit-msg 'npx --no -- commitlint --edit "$1"'
```

| Hook | Trigger | Use |
|------|---------|-----|
| `pre-commit` | Before commit | Linter, formatter |
| `commit-msg` | After message written | Validate format |
| `pre-push` | Before push | Run tests |

## Course Complete 🎉

**Recommended next steps:**
- Contribute to open source using the fork workflow (Chapter 03)
- Set up Conventional Commits + semantic-release on a personal project
- Enable branch protection on https://github.com/zaartha/thegitrepo
