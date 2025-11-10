---
title: sublation 101
---

A six-step loop from raw idea to deployed, learned-from code.

## installation
run `npx sublation-os` to install sublation-os for both cursor and claude in your project.

or install individually with:
`npx sublation-os --claude`
`npx sublation-os --cursor`

## the loop

**1. `/shape-spec`**
input: idea
output: requirements.md
resolves: ambiguity

**2. `/write-spec`**
input: requirements
output: spec.md
resolves: redundancy

**3. `/create-tasks`**
input: spec
output: tasks.md
resolves: disorder

**4. `/implement-tasks`**
input: tasks
output: code
resolves: time

**5. `/learn`**
input: observations
output: memory/*.md
resolves: forgotten patterns

## step 1: /shape-spec
clarify before design.

**input:** raw idea
**output:** requirements.md
**use when:** starting new feature, significant scope (4+ hours)

### process

1. initialize spec folder (`.sublation-os/specs/YYYY-MM-DD-feature-name/`)
2. parse requirements via 4–8 clarifying questions:
   - integration with existing functionality
   - user stories and use cases
   - visual design assets (mockups required)
   - technical constraints
   - reusable code in codebase
3. refine if gaps found

### result

`requirements.md` with answers, visual references, ready for specification.

### example

input: "add user authentication"

agent generates:
1. authentication methods? (oauth, jwt, email/password)
2. design mockups?
3. user roles needing different permissions?
4. integration with existing user model?
5. reusable auth code?

output: requirements.md with answers documented

## step 2: /write-spec
formalize design, identify reusable code.

**input:** requirements.md
**output:** spec.md
**use when:** after `/shape-spec`, before `/create-tasks`

### generates

- goal (1–2 sentences defining success)
- user stories
- core requirements
- visual design references
- reusable components with file locations
- new components required (with justifications)
- technical approach
- out of scope
- success criteria

### parse codebase

agent scans for:
- similar features already implemented
- reusable components and patterns
- existing code addressing requirement

prevents duplication. ensures consistency.

### example

reusable components found:
```
UserRepository (UserService.cs:45) — user queries
JwtTokenGenerator (AuthService.cs:120) — token generation
PasswordHasher (SecurityUtils.cs:78) — bcrypt hashing
```

leverage rather than rebuild.

## step 3: /create-tasks
structure into testable, layered groups.

**input:** spec.md
**output:** tasks.md
**use when:** after spec complete, before implementation

### generates

groups sequenced by layer and dependency:

```
task group 1: database
  1.1 write focused tests (2–8)
  1.2 create models
  1.3 create migrations
  1.4 set up associations
  1.5 verify tests pass

task group 2: api (depends on group 1)
  2.1 write focused tests
  2.2 create endpoints
  2.3 add validation

task group 3: frontend (depends on groups 1–2)
  3.1 write focused tests
  3.2 create components
  3.3 wire state
```

### principles

- focused testing: 2–8 tests per group
- layered: database → api → frontend → validation
- dependencies explicit
- acceptance criteria per group
- visual references included

## step 4: /implement-tasks
execute and verify task groups.

**input:** tasks.md, spec.md, past learnings
**output:** code, verifications/final-verification.md, new learnings
**use when:** after tasks sequenced and ready

### process

1. select task group(s)
2. build — agent:
   - reads spec, requirements, visuals
   - loads `.sublation-os/memory/`
   - implements task group
   - runs focused tests
   - tests ui in browser if applicable
   - marks tasks complete in `tasks.md`
3. verify — agent:
   - runs comprehensive verification
   - executes unit tests
   - checks against success criteria
   - generates `verifications/final-verification.md`

### auto-capture

throughout execution, agent records:
- non-obvious codebase patterns
- gotchas to avoid
- better approaches than initially planned
- architectural insights

saved to `.sublation-os/memory/` for future work.

### example

input: group 1 (database layer)

result:
```
✓ 1.1 write focused tests (5 tests)
✓ 1.2 create models (UserModel.ts)
✓ 1.3 create migrations
✓ 1.4 set up associations
✓ 1.5 verify tests pass

auto-learned:
"null-check pattern UserRepository.cs:45 applies to 3+ methods"
```

## step 5: /learn
distill observations into searchable knowledge.

**input:** session observations
**output:** memory/*.md (backend, frontend, testing, architecture, general)
**use when:** discovering patterns, fixing gotchas, gaining architectural insights

### format

each entry:

```markdown
## entry n — yyyy-mm-dd hh:mm

### context
what happened? what was the task or problem?

### lesson
the core principle as durable rule.

### application
how should future reasoning adapt? be specific.

### example (optional)
before/after or do/don't code.

### tags
searchable, tags, here
```

### categories

- backend-lessons.md — apis, databases, services
- frontend-lessons.md — ui components, state management
- testing-lessons.md — test strategies
- architecture-lessons.md — system design
- general-lessons.md — workflow, debugging

### example

```markdown
## entry 3 — 2025-11-09 14:30

### context
userrepository.cs duplicated null-checking across 3+ methods.

### lesson
explicit null-checks before accessing related entities—deliberate pattern
for handling orphaned records gracefully.

### application
when writing repository code, check userrepository.cs:45-60 before implementing
similar data access.

### example
// do
if (user != null && user.profile != null) { ... }

// don't: throws if user orphaned
var profile = user.profile;

### tags
repository-pattern, null-handling, data-access
```

## step 6: maintain
synchronize agents with all knowledge.

**input:** standards + memory files
**output:** synchronized agents
**trigger:** new standards created, 3–5 learnings recorded, new agents added, quarterly

### process

run `/update-standards-references` to propagate:

**coding standards:** style, commenting, conventions, error handling, tech stack, validation

**domain standards:** api design, migrations, database patterns, accessibility, testing

**team memory:** backend lessons, frontend patterns, testing strategies, architecture insights

updates all agents (`.claude/agents/sublation-os/*.md`, `.cursor/agents/sublation-os/*.md`) with complete reference set.

### why

without sync: agents repeat mistakes, rediscover patterns already documented.

with sync: each feature compounds knowledge. system learns itself.

## the loop in sequence

```
/shape-spec
  → requirements.md

/write-spec
  → spec.md (identifies reusable components)

/create-tasks
  → tasks.md (database → api → frontend → testing)

/implement-tasks
  → code, verifications, learnings

/learn
  → memory/*.md entries

maintain
  → all agents synchronized
```

## recursion

traditional loop:
```
idea → code → bugs → ship
```

sublation loop:
```
idea → requirements → spec → tasks → implementation → lessons → better spec
```

the loop closes when knowledge becomes reference.
every feature feeds the next.
the system learns itself.

## related

- [[context engineering]] – managing context windows for AI agents
- [[extract PR feedback into institutional knowledge]] – learning from code review