---
title: sublation 101
---

A six-step loop from raw idea to deployed, learned-from code.

---

## the loop

**1. `/shape-spec`**
Input: Idea
Output: requirements.md
Resolves: Ambiguity

**2. `/write-spec`** 
Input: Requirements
Output: spec.md
Resolves: Redundancy

**3. `/create-tasks`**
Input: Spec
Output: tasks.md
Resolves: Disorder

**4. `/implement-tasks`**
Input: Tasks 
Output: Code 
Resolves: Time

**5. `/learn`** 
Input: Observations 
Output: memory/*.md 
Resolves: Forgotten patterns

---

## step 1: /shape-spec
Clarify before design.

**Input:** Raw idea
**Output:** requirements.md
**Use when:** Starting new feature, significant scope (4+ hours)

### process

1. Initialize spec folder (`.sublation-os/specs/YYYY-MM-DD-feature-name/`)
2. Parse requirements via 4–8 clarifying questions:
   - Integration with existing functionality
   - User stories and use cases
   - Visual design assets (mockups required)
   - Technical constraints
   - Reusable code in codebase
3. Refine if gaps found

### result

`requirements.md` with answers, visual references, ready for specification.

### example

Input: "Add user authentication"

Agent generates:
1. Authentication methods? (OAuth, JWT, email/password)
2. Design mockups?
3. User roles needing different permissions?
4. Integration with existing user model?
5. Reusable auth code?

Output: requirements.md with answers documented

---

## step 2: /write-spec
Formalize design, identify reusable code.

**Input:** requirements.md
**Output:** spec.md
**Use when:** After `/shape-spec`, before `/create-tasks`

### generates

- Goal (1–2 sentences defining success)
- User stories
- Core requirements
- Visual design references
- Reusable components with file locations
- New components required (with justifications)
- Technical approach
- Out of scope
- Success criteria

### parse codebase

Agent scans for:
- Similar features already implemented
- Reusable components and patterns
- Existing code addressing requirement

Prevents duplication. Ensures consistency.

### example

Reusable components found:
```
UserRepository (UserService.cs:45) — user queries
JwtTokenGenerator (AuthService.cs:120) — token generation
PasswordHasher (SecurityUtils.cs:78) — bcrypt hashing
```

Leverage rather than rebuild.

---

## step 3: /create-tasks
Structure into testable, layered groups.

**Input:** spec.md
**Output:** tasks.md
**Use when:** After spec complete, before implementation

### generates

Groups sequenced by layer and dependency:

```
Task Group 1: Database
  1.1 Write focused tests (2–8)
  1.2 Create models
  1.3 Create migrations
  1.4 Set up associations
  1.5 Verify tests pass

Task Group 2: API (depends on Group 1)
  2.1 Write focused tests
  2.2 Create endpoints
  2.3 Add validation

Task Group 3: Frontend (depends on Groups 1–2)
  3.1 Write focused tests
  3.2 Create components
  3.3 Wire state
```

### principles

- Focused testing: 2–8 tests per group
- Layered: database → API → frontend → validation
- Dependencies explicit
- Acceptance criteria per group
- Visual references included

---

## step 4: /implement-tasks
Execute and verify task groups.

**Input:** tasks.md, spec.md, past learnings
**Output:** Code, verifications/final-verification.md, new learnings
**Use when:** After tasks sequenced and ready

### process

1. Select task group(s)
2. Build — agent:
   - Reads spec, requirements, visuals
   - Loads `.sublation-os/memory/`
   - Implements task group
   - Runs focused tests
   - Tests UI in browser if applicable
   - Marks tasks complete in `tasks.md`
3. Verify — agent:
   - Runs comprehensive verification
   - Executes unit tests
   - Checks against success criteria
   - Generates `verifications/final-verification.md`

### auto-capture

Throughout execution, agent records:
- Non-obvious codebase patterns
- Gotchas to avoid
- Better approaches than initially planned
- Architectural insights

Saved to `.sublation-os/memory/` for future work.

### example

Input: Group 1 (database layer)

Result:
```
✓ 1.1 Write focused tests (5 tests)
✓ 1.2 Create models (UserModel.ts)
✓ 1.3 Create migrations
✓ 1.4 Set up associations
✓ 1.5 Verify tests pass

Auto-learned:
"Null-check pattern UserRepository.cs:45 applies to 3+ methods"
```

---

## step 5: /learn
Distill observations into searchable knowledge.

**Input:** Session observations
**Output:** memory/*.md (backend, frontend, testing, architecture, general)
**Use when:** Discovering patterns, fixing gotchas, gaining architectural insights

### format

Each entry:

```markdown
## Entry N — YYYY-MM-DD HH:mm

### Context
What happened? What was the task or problem?

### Lesson
The core principle as durable rule.

### Application
How should future reasoning adapt? Be specific.

### example (Optional)
Before/after or do/don't code.

### Tags
searchable, tags, here
```

### categories

- backend-lessons.md — APIs, databases, services
- frontend-lessons.md — UI components, state management
- testing-lessons.md — Test strategies
- architecture-lessons.md — System design
- general-lessons.md — Workflow, debugging

### example

```markdown
## Entry 3 — 2025-11-09 14:30

### Context
UserRepository.cs duplicated null-checking across 3+ methods.

### Lesson
Explicit null-checks before accessing related entities—deliberate pattern
for handling orphaned records gracefully.

### Application
When writing repository code, check UserRepository.cs:45-60 before implementing
similar data access.

### example
// DO
if (user != null && user.Profile != null) { ... }

// DON'T: throws if user orphaned
var profile = user.Profile;

### Tags
repository-pattern, null-handling, data-access
```

---

## step 6: maintain
Synchronize agents with all knowledge.

**Input:** Standards + memory files
**Output:** Synchronized agents
**Trigger:** New standards created, 3–5 learnings recorded, new agents added, quarterly

### process

Run `/update-standards-references` to propagate:

**Coding Standards:** Style, commenting, conventions, error handling, tech stack, validation

**Domain Standards:** API design, migrations, database patterns, accessibility, testing

**Team Memory:** Backend lessons, frontend patterns, testing strategies, architecture insights

Updates all agents (`.claude/agents/sublation-os/*.md`, `.cursor/agents/sublation-os/*.md`) with complete reference set.

### why

Without sync: agents repeat mistakes, rediscover patterns already documented.

With sync: each feature compounds knowledge. System learns itself.

---

## the loop in sequence

```
/shape-spec
  → requirements.md

/write-spec
  → spec.md (identifies reusable components)

/create-tasks
  → tasks.md (database → API → frontend → testing)

/implement-tasks
  → Code, verifications, learnings

/learn
  → memory/*.md entries

Maintain
  → All agents synchronized
```

---

## recursion

Traditional loop:
```
Idea → Code → Bugs → Ship
```

Sublation loop:
```
Idea → Requirements → Spec → Tasks → Implementation → Lessons → Better Spec
```

The loop closes when knowledge becomes reference.
Every feature feeds the next.
The system learns itself.