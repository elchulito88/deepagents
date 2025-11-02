# Development Workflow Rules

This document defines the hard rules for working on this repository.

## Git Workflow

### 1. Feature Branches (REQUIRED)
- **Always** create a feature branch for new changes
- Never commit directly to `master`
- Branch naming: `feature/descriptive-name`

### 2. Local Merges Only (REQUIRED)
- All merges go to **your local master branch** (`elchulito88/deepagents`)
- **NEVER** create PRs to upstream (`langchain-ai/deepagents`) unless explicitly requested
- This is your fork - keep development local

### 3. Delete Merged Branches (REQUIRED)
- **ALWAYS** delete feature branches immediately after merging
- Delete both local and remote branches
- No stale branches should remain

### 4. Documentation Guidelines (REQUIRED)
- Create only essential user-facing documentation
- **AVOID** creating excessive markdown files
- **DO NOT** create exploration/analysis files (e.g., CODEBASE_OVERVIEW.md, EXPLORATION_SUMMARY.md)
- Keep docs minimal and focused on features

## Standard Workflow

```bash
# 1. Create feature branch from master
git checkout master
git checkout -b feature/new-feature

# 2. Make changes, test, and commit
git add .
git commit -m "feat: description"

# 3. Push to YOUR fork
git push -u origin feature/new-feature

# 4. Merge to YOUR master (local)
git checkout master
git merge feature/new-feature --no-ff

# 5. Push YOUR master
git push origin master

# 6. DELETE feature branch immediately (REQUIRED)
git branch -d feature/new-feature
git push origin --delete feature/new-feature
```

## Testing Requirements

- Write unit tests for new features
- Run existing tests before merging
- Document test coverage in commit messages

## Commit Message Format

```
<type>: <description>

<optional body>

🤖 Generated with [Claude Code](https://claude.com/claude-code)

Co-Authored-By: Claude <noreply@anthropic.com>
```

Types: `feat`, `fix`, `docs`, `test`, `refactor`, `chore`

---

**These rules are mandatory for all development on this repository.**
