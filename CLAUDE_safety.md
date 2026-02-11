# Zordon Oracle - Safety Rules

## Git Safety (CRITICAL)

### NEVER Do
- `git push --force` — Destroys history
- `git push origin main` — Always use feature branch + PR
- `git commit --amend` — Breaks hash references
- `git reset --hard` — Destroys uncommitted work
- `git checkout .` — Discards all changes
- `git clean -f` — Deletes untracked files
- `--no-verify` — Never skip hooks

### ALWAYS Do
- Create feature branch for all changes
- Create PR and wait for human approval
- Commit with descriptive messages
- Check `git status` before committing

## PR Workflow

```
1. git checkout -b feat/description
2. git add [specific files]
3. git commit -m "descriptive message"
4. git push -u origin feat/description
5. gh pr create --title "..." --body "..."
6. WAIT for human review and merge
```

## File Safety

- **Never delete files** without explicit permission
- **Never modify files** outside this repo without notification
- **Never create temp files** outside `.tmp/` directory
- **Always use `.gitignore`** to prevent tracking sensitive/temp files

## Data Safety

- **Never commit secrets** (.env, credentials, API keys)
- **Never commit large binaries** (>1MB)
- **Check before committing** — `git diff --staged`
