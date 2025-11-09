---
title: extract PR feedback into institutional knowledge
---

# learn from code review

Extract review insights from GitHub PRs. Parse patterns. Preserve lessons. Prevent regressions.

---

## setup: github cli

### install

**Install via:**
```bash
# Windows
winget install --id GitHub.cli

# macOS
brew install gh

# Linux: apt install gh | dnf install gh
```

### authenticate

```bash
gh auth login
# Select GitHub.com → HTTPS → Web browser login
```

Verify:
```bash
gh auth status
gh pr list --limit 5
```

---

## step 1: fetch recent prs

```
can you fetch the 10 most recent prs opened by me?
```

Claude Code executes:
```bash
gh pr list --author=@me --limit 10
```

Returns: PR number, title, branch, status, date.

---

## step 2: filter merged + reviewed

```
can you get only the ones merged and that received review comments?
```

Claude Code:
1. Fetch merged PRs: `gh pr list --author=@me --state merged --limit 50`
2. Check review counts: `gh pr view $pr --json reviews | jq '.reviews | length'`

Returns table: PR #, title, review count.

High review counts (10+) signal complexity. These PRs contain learning opportunities.

---

## step 3: retrieve review comments

```
can you retrieve all the comments in context so that we can learn from them?
```

Claude Code:
```bash
gh pr view 18642 --json reviews
gh pr view 18642 --json comments
```

Analyzes patterns across PRs. Compiles into REVIEW_LEARNINGS.md.

---

## output: review_learnings.md

Generated document structure:

```

**Key themes:**
- Performance optimization (N+1 queries, batch operations)
- Database function consolidation (remove legacy, feature flags)
- Test coverage (>100% on new code, edge cases)
- Backward compatibility (design for migration)
- Code generation sync (XML, SQL table types)

---

## step 4: capture critical lessons

```
/sublation-os:learn Learn from the PR feedback. Only learn critical comments about coding.
```

Claude Code:
1. Parses REVIEW_LEARNINGS.md
2. Extracts coding patterns (not generic advice)
3. Creates structured lessons:
   - Context
   - Lesson
   - Application (steps)
   - Example (before/after)
   - Tags (searchable)
4. Appends to `.sublation-os/memory/backend-lessons.md`

**Example: N+1 Query Performance**

**Lesson:** Always batch database queries. Never loop + fetch. Use SQL TVP (table-valued parameters).

**Application:**
1. Create SQL table type: `CREATE TYPE IntegerKeyTableType AS TABLE ([Key] INT)`
2. Create batch function: `fnGetWorkItemUserProfileActorsBatch`
3. Update CodeGenSettings.xml

**Tags:** `performance`, `N+1 queries`, `batch operations`

---

## step 5: apply learnings

Search lessons before coding:
```
/sublation-os:recall N+1 queries
```

Or reference during implementation:
```
/sublation-os:update-standards-references batch operations
```

---

## workflow loop

```
Fetch PRs → Filter Reviewed → Parse Comments → Extract Lessons → Apply Lessons → Better PRs → Faster Approvals
```

Each feature submission redefines the system that builds it.

---

## commands

**GitHub CLI:**
```bash
gh pr list --author=@me --limit 10                    # List your PRs
gh pr list --state merged --limit 50                  # Merged only
gh pr view 18642 --json reviews,comments              # PR details
gh pr view 18642 --json reviews --jq '.reviews | length'  # Review count
```

**Sublation-OS:**
```
/sublation-os:learn [instruction]              # Capture learning
/sublation-os:recall [keyword]                 # Search lessons
/sublation-os:update-standards-references      # Sync references
```

---

## result

Scattered review comments → Structured knowledge. Searchable by tag. Persistent across sessions.

Patterns emerge. Mistakes prevent. Code improves. Approvals accelerate.
