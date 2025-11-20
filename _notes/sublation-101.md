---
title: sublation 101
---

A development framework that turns vague ideas into working code while building institutional knowledge.

## what is sublation-os?

sublation-os is a framework for AI-assisted development that provides:

- **structured workflow**: six commands that guide features from idea to code
- **persistent memory**: lessons from each session feed into future work
- **specialized agents**: AI assistants that handle planning, implementation, and verification
- **coding standards**: customizable guidelines that keep your codebase consistent

**compatible with**: Claude Code and Cursor AI editors

sublation-os is a fork of the original [buildermethods/agentos](https://github.com/buildermethods/agentos) system, adapted and extended for broader use cases.

## installation

install sublation-os in your project with one command:

```bash
npx sublation-os
```

this creates three directories in your project:
- `.sublation-os/` - core framework (memory, specs, standards)
- `.claude/` - claude code integration (agents and commands)
- `.cursor/` - cursor integration (commands)

you can also install for specific tools:
```bash
npx sublation-os --claude  # claude code only
npx sublation-os --cursor  # cursor only
```

## prerequisites

before installing sublation-os, ensure you have:

- **node.js**: version 16 or higher
- **npm or npx**: for running the installation command
- **git repository**: sublation-os works best in git-tracked projects
- **AI editor**: Claude Code or Cursor installed and configured

## key concepts

understanding these terms will help you navigate the workflow:

- **spec**: a specification document that describes what you're building, why, and how. stored in `.sublation-os/specs/[date]-[feature-name]/`
- **agents**: AI assistants with specialized roles (spec-shaper, implementer, verifier). each agent has specific knowledge and tools for its task
- **memory**: persistent lessons stored in `.sublation-os/memory/` that feed into future work. organized by category (backend, frontend, testing, etc.)
- **standards**: coding guidelines in `.sublation-os/standards/` that keep your codebase consistent. agents reference these during implementation
- **task groups**: ordered sets of implementation tasks, organized by architectural layer (database → api → frontend)

## the six-step workflow

each feature flows through six commands. each command solves a specific problem.

**core workflow**: steps 1-4 (shape → spec → tasks → implement) form the essential path.
**maintenance steps**: steps 5-6 (learn → consolidate) are optional but recommended for knowledge retention.

**1. `/shape-spec`** - clarify the idea
- **input**: rough feature idea
- **output**: requirements.md with answered questions
- **solves**: ambiguity about what you're building

**2. `/write-spec`** - formalize the design
- **input**: requirements.md
- **output**: spec.md with detailed design
- **solves**: redundant work by finding reusable code

**3. `/create-tasks`** - break into steps
- **input**: spec.md
- **output**: tasks.md with ordered task groups
- **solves**: overwhelm from large features

**4. `/implement-tasks`** - build it
- **input**: tasks.md
- **output**: working code + verification report
- **solves**: implementation time and verification

**5. `/learn`** - capture insights
- **input**: observations from building
- **output**: memory/*.md lesson entries
- **solves**: repeating the same mistakes

**6. `/consolidate-learnings`** - sync knowledge
- **input**: standards + memory files
- **output**: agents with current knowledge
- **solves**: agents forgetting past learnings

## step 1: /shape-spec

turn a rough idea into clear requirements.

**when to use**: starting any non-trivial feature that requires multiple files, components, or layers. skip for simple bug fixes or single-function changes.

**what it does**:
1. creates a dated spec folder: `.sublation-os/specs/YYYY-MM-DD-feature-name/`
2. asks you 4-8 clarifying questions about your idea
3. prompts you for visual assets (mockups, screenshots)
4. saves everything to `planning/requirements.md`

**what you get**:
- clear answers to ambiguous parts of your idea
- visual references stored in `planning/visuals/`
- foundation for the detailed spec

**the agent asks about**:
- how this integrates with existing code
- user stories and use cases
- visual design and mockups
- technical constraints
- what code already exists that you can reuse

**example**:

you say: "add user authentication"

the agent asks:
1. which authentication method? (oauth, jwt, email/password)
2. do you have design mockups?
3. are there different user roles with different permissions?
4. does a user model already exist?
5. is there existing auth code we can reuse?

you answer these questions, and the agent saves your responses to `requirements.md`.

## step 2: /write-spec

create a detailed specification document.

**when to use**: after `/shape-spec`, before writing any code

**what it does**:
1. reads your `requirements.md` and visual assets
2. scans your codebase for existing patterns and reusable code
3. creates a comprehensive `spec.md` in your spec folder

**what the spec includes**:
- **goal**: 1-2 sentences defining success
- **user stories**: who does what and why
- **core requirements**: must-have features
- **visual references**: links to mockups
- **reusable components**: existing code you can use (with file paths)
- **new components**: what needs to be built (with justifications)
- **technical approach**: how you'll build it
- **out of scope**: what you're explicitly not doing
- **success criteria**: how you'll know it works

**why this matters**:

the agent scans your codebase to find:
- similar features you've already built
- components and patterns you can reuse
- existing code that solves part of the problem

this prevents rebuilding things you already have and keeps your code consistent.

**example**:

for user authentication, the agent might find:

```
reusable components:
- UserRepository (UserService.cs:45) - handles user queries
- JwtTokenGenerator (AuthService.cs:120) - creates auth tokens
- PasswordHasher (SecurityUtils.cs:78) - secure password hashing

new components needed:
- LoginController - handles auth endpoints
- AuthMiddleware - validates tokens on requests
```

you leverage existing code instead of rebuilding from scratch.

## step 3: /create-tasks

break the spec into ordered, testable task groups.

**when to use**: after `/write-spec`, before implementation

**what it does**:
1. reads your `spec.md`
2. breaks the work into logical groups
3. orders groups by dependencies (database → api → frontend)
4. creates `tasks.md` with checkbox lists

**how tasks are organized**:

tasks are grouped by architectural layer. groups run in sequence:

```
task group 1: database layer
  - [ ] 1.1 write focused tests (2-8 tests)
  - [ ] 1.2 create models
  - [ ] 1.3 create migrations
  - [ ] 1.4 set up associations
  - [ ] 1.5 verify tests pass

task group 2: api layer (depends on group 1)
  - [ ] 2.1 write focused tests
  - [ ] 2.2 create endpoints
  - [ ] 2.3 add validation

task group 3: frontend layer (depends on groups 1-2)
  - [ ] 3.1 write focused tests
  - [ ] 3.2 create components
  - [ ] 3.3 wire state management
```

**key principles**:
- **focused tests**: 2-8 tests per group (not exhaustive, just focused)
- **layered approach**: build from bottom up (database → api → frontend)
- **explicit dependencies**: each group lists what it depends on
- **acceptance criteria**: each group defines "done"
- **visual references**: mockups linked where relevant

**why this matters**:

instead of jumping into code, you have a clear roadmap. you build the foundation first, then the layers on top. when something breaks, you know which layer has the problem.

## step 4: /implement-tasks

build the feature and verify it works.

**when to use**: after `/create-tasks` creates your task list

**what it does**:

this is a multi-phase process:

**phase 1: select task groups**
- you tell the agent which task group(s) to implement
- or tell it to implement all groups

**phase 2: implement with specialized agents**
- **implementer agent** builds the code:
  - reads spec, requirements, and visuals
  - loads past learnings from `.sublation-os/memory/`
  - implements the task group
  - runs focused tests
  - tests UI in browser if needed
  - marks tasks complete with `[x]` in `tasks.md`

**phase 3: verify the implementation**
- **implementation-verifier agent** runs when ALL tasks complete:
  - runs comprehensive tests
  - checks against success criteria from spec
  - generates `verifications/final-verification.md`
  - if verification fails: reports issues and you can fix them before moving to the next feature

**automatic learning**:

while implementing, the agent notices and captures:
- codebase patterns that aren't obvious
- gotchas and things to avoid
- better approaches than originally planned
- architectural insights

these get saved to `.sublation-os/memory/` automatically as the agent works.

**example**:

you run: `/implement-tasks`

agent implements group 1 (database layer):
```
- [x] 1.1 write focused tests (5 tests written)
- [x] 1.2 create models (UserModel.ts)
- [x] 1.3 create migrations (001_create_users.sql)
- [x] 1.4 set up associations
- [x] 1.5 verify tests pass

automatically learned:
"null-check pattern in UserRepository.cs:45 applies to 3+ methods.
future repository code should follow this pattern."
```

the learning gets saved to `.sublation-os/memory/backend-lessons.md` automatically.

## step 5: /learn

manually capture important lessons for future sessions.

**when to use**:
- discovered a non-obvious pattern
- fixed a tricky bug
- learned something that future sessions should know
- found a gotcha to avoid

**note**: `/implement-tasks` already captures learnings automatically as it works. use `/learn` when you want to manually document something important that wasn't auto-captured, or to add additional context to automatic learnings.

**what it does**:
1. asks you about what you learned
2. formats it as a structured entry
3. saves it to the appropriate memory file

**memory categories**:
- `backend-lessons.md` - apis, databases, services
- `frontend-lessons.md` - ui components, state management
- `testing-lessons.md` - test strategies
- `architecture-lessons.md` - system design
- `general-lessons.md` - workflow, debugging

**entry format**:

each learning follows this structure:

```markdown
## entry n - yyyy-mm-dd hh:mm

### context
what happened? what was the task or problem?

### lesson
the core principle as a durable rule.

### application
how should future work adapt? be specific about:
- which files/services/patterns this applies to
- what to check before making similar changes
- what approaches work best

### example (optional)
concrete before/after or do/don't code.

### tags
searchable, tags, here
```

**example entry**:

```markdown
## entry 3 - 2025-11-09 14:30

### context
userrepository.cs had duplicated null-checking across 3+ methods.

### lesson
explicit null-checks before accessing related entities is a deliberate
pattern for handling orphaned records gracefully.

### application
when writing repository code, check userrepository.cs:45-60 before
implementing similar data access. always null-check both parent and
related entities.

### example
// do this
if (user != null && user.profile != null) {
    return user.profile;
}

// don't do this - throws if user orphaned
var profile = user.profile;

### tags
repository-pattern, null-handling, data-access
```

**why this matters**:

these lessons load into future claude sessions. when you run `/implement-tasks` later, the agent reads all your memory files and applies these lessons to new work.

## step 6: /consolidate-learnings

ensure all agents have access to your complete knowledge base.

**when to use**:
- after creating new standards files
- after recording 3-5 new learnings
- when you notice agents missing recent context or repeating old mistakes
- when adding new agents to your workflow

**the problem it solves**:

sublation-os agents reference files using `@file-path` syntax (e.g., `@.sublation-os/standards/backend/api-design.md`) in their configuration. this tells the AI to load those files as context when the agent runs. when you add a new standard or memory file, agents that already reference some files need to reference ALL files to have complete context.

**what it does**:

scans all your agents and ensures they reference:
- **all standards files** from `.sublation-os/standards/`
  - global: conventions, commenting, naming
  - backend: apis, databases, error handling
  - frontend: components, state management, styling
  - testing: test writing, mocking strategies
- **all memory files** from `.sublation-os/memory/`
  - backend-lessons.md
  - frontend-lessons.md
  - testing-lessons.md
  - architecture-lessons.md
  - general-lessons.md

**how it works**:

1. finds all agents that reference at least one standard or memory file
2. checks which files each agent is missing
3. adds the missing references to each agent
4. generates a report of what was updated

**example output**:

```
implementer.md - added references:
  • .sublation-os/standards/backend/queries.md
  • .sublation-os/standards/testing/test-writing.md
  • .sublation-os/memory/architecture-lessons.md

spec-shaper.md - added references:
  • .sublation-os/standards/global/conventions.md

all other agents have complete references
```

**why this matters**:

without sync: agents work with incomplete knowledge. they repeat mistakes or rediscover patterns you've already documented.

with sync: every feature builds on accumulated knowledge. the system learns from itself.

## putting it all together

here's a complete feature flow:

```
idea: "add user authentication"
    ↓
/shape-spec
    → .sublation-os/specs/2025-11-20-user-auth/planning/requirements.md
    → agent asks clarifying questions, you answer
    ↓
/write-spec
    → .sublation-os/specs/2025-11-20-user-auth/spec.md
    → agent scans codebase, finds reusable components
    ↓
/create-tasks
    → .sublation-os/specs/2025-11-20-user-auth/tasks.md
    → tasks grouped by layer (database → api → frontend)
    ↓
/implement-tasks
    → working code
    → .sublation-os/specs/2025-11-20-user-auth/verifications/final-verification.md
    → learnings auto-saved to .sublation-os/memory/
    ↓
/learn (optional)
    → manually capture additional lessons
    ↓
/consolidate-learnings
    → agents get new learnings for next feature
```

## the compounding effect

**traditional workflow**:
```
idea → code → bugs → ship → (knowledge lost)
```

**sublation workflow**:
```
idea → requirements → spec → tasks → code → lessons → (knowledge persists)
```

the difference:
- **feature 1**: takes normal time, captures patterns
- **feature 2**: faster because it reuses patterns from feature 1
- **feature 3**: even faster because it builds on features 1 and 2
- **feature n**: feels like the codebase builds itself

each feature makes the next one easier. knowledge compounds instead of resets.

## the key insight

sublation-os doesn't just help you build features. it helps your development environment learn from experience.

standards + memory + verification = a development system that gets smarter with use.

## related

- [[context engineering]] - managing context windows for AI agents
- [[extract PR feedback into institutional knowledge]] - learning from code review