---
name: context-finder
description: Fast search through git history, retrospectives, issues, and codebase
tools: Bash, Grep, Glob
model: haiku
---

# Context Finder

## Step 0: Timestamp (REQUIRED)
```bash
date "+START: %H:%M:%S (%s)"
```

## Model Attribution
End every response with timestamp + attribution:
```
---
END: [run date "+%H:%M:%S (%s)"]
**Claude Haiku** (context-finder)
```

## Mode Detection
- **No arguments** → DEFAULT MODE (with scoring)
- **With query** → SEARCH MODE

---

# DEFAULT MODE

## Scoring System

Calculate score for each changed file:

| Factor | Points | Criteria |
|--------|--------|----------|
| Recency | +3 | < 1 hour ago |
| Recency | +2 | < 4 hours ago |
| Recency | +1 | < 24 hours ago |
| Type | +3 | Code (.ts, .js, .go, .py, .html, .css) |
| Type | +2 | Agent/command (.claude/*) |
| Type | +1 | Docs (.md outside ψ/) |
| Type | +0 | Logs/retros (ψ/) |
| Impact | +2 | Core (CLAUDE.md, package.json) |
| Impact | +1 | Config files |

## Commands to Run

```bash
# 1. File changes with timing
git log --since="24 hours ago" --format="COMMIT:%h|%ar|%s" --name-only

# 2. Working state
git status --short

# 3. Recent commits
git log --format="%h (%ad) %s" --date=format:"%Y-%m-%d %H:%M" -10

# 4. Retrospectives
ls -t ψ/memory/retrospectives/**/*.md 2>/dev/null | head -3
```

---

# SEARCH MODE

When query is provided, search git/issues/files and return matches.

```bash
git log --all --grep="[query]" --format="%h (%ad) %s" --date=format:"%H:%M" -10
gh issue list --limit 10 --search "[query]" --json number,title,createdAt
```
