---
title: extract PR feedback into institutional knowledge
---

extract review insights from github prs. parse patterns. preserve lessons. prevent regressions.

## setup: github cli

### install

**install via:**
```bash
# windows
winget install --id GitHub.cli

# macos
brew install gh

# linux: apt install gh | dnf install gh
```

### authenticate

```bash
gh auth login
# select github.com → https → web browser login
```

verify:
```bash
gh auth status
gh pr list --limit 5
```

## step 1: fetch recent prs

```
can you fetch the 10 most recent prs opened by me?
```

claude code executes:
```bash
gh pr list --author=@me --limit 10
```

returns: pr number, title, branch, status, date.

## step 2: filter merged + reviewed

```
can you get only the ones merged and that received review comments?
```

claude code:
1. fetch merged prs: `gh pr list --author=@me --state merged --limit 50`
2. check review counts: `gh pr view $pr --json reviews | jq '.reviews | length'`

returns table: pr #, title, review count.

high review counts (10+) signal complexity. these prs contain learning opportunities.

## step 3: retrieve review comments

```
can you retrieve all the comments in context so that we can learn from them?
```

claude code:
```bash
gh pr view 18642 --json reviews
gh pr view 18642 --json comments
```

analyzes patterns across prs. compiles into review_learnings.md.

## output: review_learnings.md

generated document structure:

**key themes:**
- performance optimization (n+1 queries, batch operations)
- database function consolidation (remove legacy, feature flags)
- test coverage (>100% on new code, edge cases)
- backward compatibility (design for migration)
- code generation sync (xml, sql table types)

## step 4: capture critical lessons

```
/sublation-os:learn learn from the pr feedback. only learn critical comments about coding.
```

claude code:
1. parses review_learnings.md
2. extracts coding patterns (not generic advice)
3. creates structured lessons:
   - context
   - lesson
   - application (steps)
   - example (before/after)
   - tags (searchable)
4. appends to `.sublation-os/memory/backend-lessons.md`

**example: n+1 query performance**

**lesson:** always batch database queries. never loop + fetch. use sql tvp (table-valued parameters).

**application:**
1. create sql table type: `create type integerkeyTabletype as table ([key] int)`
2. create batch function: `fngetworkitemuserprofileactorsbatch`
3. update codegensettings.xml

**tags:** `performance`, `n+1 queries`, `batch operations`

## step 5: apply learnings

search lessons before coding:
```
/sublation-os:recall n+1 queries
```

or reference during implementation:
```
/sublation-os:consolidate-learnings batch operations
```

## workflow loop

```
fetch prs → filter reviewed → parse comments → extract lessons → apply lessons → better prs → faster approvals
```

each feature submission redefines the system that builds it.

## commands

**github cli:**
```bash
gh pr list --author=@me --limit 10                    # list your prs
gh pr list --state merged --limit 50                  # merged only
gh pr view 18642 --json reviews,comments              # pr details
gh pr view 18642 --json reviews --jq '.reviews | length'  # review count
```

**sublation-os:**
```
/sublation-os:learn [instruction]              # capture learning
/sublation-os:recall [keyword]                 # search lessons
/sublation-os:consolidate-learnings            # sync references
```

## result

scattered review comments → structured knowledge. searchable by tag. persistent across sessions.

patterns emerge. mistakes prevent. code improves. approvals accelerate.

## related

- [[sublation 101]] – the six-step loop for feature development
- [[context engineering]] – managing AI agent context windows
