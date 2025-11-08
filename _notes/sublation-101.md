---
title: The Sublation-OS Feature Development Workflow
---
# The Sublation-OS Feature Development Workflow

A complete guide to building features using sublation-os's six-step framework.

---

## Overview

Sublation-OS provides a structured, AI-assisted workflow for developing features from initial idea to deployed, documented, and learned-from code. The process is designed to keep humans in control of decisions while leveraging AI for research, specification writing, task breakdown, and implementation.

The six-step workflow is:

1. **Shape-Spec** — Gather requirements through targeted research
2. **Write-Spec** — Create a detailed specification document
3. **Create-Tasks** — Break the specification into implementation tasks
4. **Implement-Tasks** — Build the feature with AI assistance
5. **Learn** — Capture lessons for future work
6. **Update-Standards** — Maintain team standards and consistency

---

## Step 1: Shape-Spec — Gather Requirements

**Command**: `/shape-spec`

### What It Does

The `shape-spec` command orchestrates a three-phase requirement-gathering process that ensures you have a clear, comprehensive understanding of what you're building before you start designing it.

### The Three Phases

#### Phase 1: Initialize Spec Folder
Your spec is created in a timestamped folder: `.sublation-os/specs/YYYY-MM-DD-feature-name/`

This folder becomes the home for all specification, planning, and verification artifacts.

#### Phase 2: Ask Clarifying Questions
The spec-shaper agent asks 4-8 numbered questions about your feature, including:

- How it integrates with existing functionality
- User stories and use cases
- Visual design requirements (it will ask you to show mockups)
- Technical constraints or dependencies
- Reusability opportunities from existing code

The agent **mandatorily checks** for visual assets (mockups, wireframes, screenshots) in your `planning/visuals/` directory. This ensures design is considered from the start.

Your answers are compiled into `planning/requirements.md`.

#### Phase 3: Follow-Up (If Needed)
If gaps are found, the agent asks targeted follow-up questions to complete the picture.

### Outputs

- `planning/initialization.md` — Your raw feature idea
- `planning/requirements.md` — Comprehensive requirements with Q&A
- `planning/visuals/` — Visual assets directory (you add images/mockups)

### When to Use

- Starting a new feature
- Adding a significant capability to your product
- Any work that takes 4+ hours to implement

### Example Flow

```
You: "I want to add user authentication"

Agent:
1. What authentication methods? (OAuth, JWT, email/password?)
2. Do you have design mockups? (shows visual asset check)
3. What user roles need different permissions?
4. How does this integrate with the existing user model?
5. Are there reusable auth libraries in the codebase already?

You provide answers → requirements.md is created
```

---

## Step 2: Write-Spec — Create the Specification

**Command**: `/write-spec`

### What It Does

The `write-spec` command transforms your gathered requirements into a detailed specification document that developers (human or AI) use to guide implementation.

### The Specification Document

The spec-writer agent creates `spec.md` with these sections:

**Goal** — 1-2 sentences defining what success looks like

**User Stories** — How real users will interact with the feature

**Core Requirements** — Essential must-haves

**Visual Design** — Reference to your mockups and design approach

**Reusable Components** — Existing code and patterns to leverage

**New Components Required** — What needs to be built new (with justifications)

**Technical Approach** — How you'll build it

**Out of Scope** — What's explicitly NOT included

**Success Criteria** — How you'll verify it works

### Key Feature: Codebase Analysis

Before writing specs, the agent searches your codebase for:
- Similar features already implemented
- Reusable components and patterns
- Existing code that addresses part of the requirement

This prevents duplicate work and maintains consistency.

### Outputs

- `spec.md` — Developer-ready specification document

### When to Use

After completing `/shape-spec` and before `/create-tasks`

### Example Section

```markdown
## Reusable Components

The codebase already has:
- UserRepository (UserService.cs:45) — handles user queries
- JwtTokenGenerator (AuthService.cs:120) — generates tokens
- PasswordHasher (SecurityUtils.cs:78) — bcrypt hashing

We should leverage these rather than rebuild.
```

---

## Step 3: Create-Tasks — Break Into Implementation Chunks

**Command**: `/create-tasks`

### What It Does

The `create-tasks` command transforms your specification into a structured breakdown of implementation tasks organized by development layer (database, API, frontend, testing).

### Task Organization

Tasks are grouped by specialization and sequenced with dependencies:

```
### Task Group 1: Database Layer
  1.0 Complete database layer
    1.1 Write focused tests (2-8 tests)
    1.2 Create database models
    1.3 Create migrations
    1.4 Set up associations
    1.5 Ensure tests pass

### Task Group 2: API Layer (depends on Group 1)
  2.0 Complete API layer
    2.1 Write focused tests
    2.2 Create endpoints
    2.3 Add validation
    ...
```

### Key Principles

- **Focused Testing**: 2-8 tests per task group, not exhaustive coverage
- **Layered Approach**: Database → API → Frontend → Testing
- **Dependencies Noted**: Clear order of implementation
- **Acceptance Criteria**: Each group has specific success criteria
- **Visual References**: Links to design assets when relevant

### Outputs

- `tasks.md` — Grouped, ordered list of implementation tasks

### When to Use

After `spec.md` is complete and before assigning implementation work

---

## Step 4: Implement-Tasks — Build the Feature

**Command**: `/implement-tasks`

### What It Does

The `implement-tasks` command oversees the actual implementation of one or more task groups, running code verification and automatically capturing learnings.

### The Three Phases

#### Phase 1: Select Task Group(s)

You choose which task group(s) to implement. You can:
- Implement them sequentially (Task Group 1, then Task Group 2, etc.)
- Implement multiple groups if they're independent
- Spread implementation across multiple sessions

#### Phase 2: Implement

The implementer agent:
- Analyzes the spec.md, requirements.md, and visual assets
- Loads past learnings from `.sublation-os/memory/` to understand codebase patterns
- Implements the assigned task group
- Runs the focused tests written for that group
- If UI work: opens browser and tests as an end user
- Marks completed tasks with checkmarks in `tasks.md`

#### Phase 3: Verify

Once ALL tasks are marked complete, the implementation-verifier agent:
- Runs comprehensive verification
- Tests end-to-end functionality
- Checks against success criteria
- Creates a verification report: `verifications/final-verification.md`

### Automatic Learning Capture

Throughout implementation, the agent automatically captures institutional knowledge via the **auto-learn skill** when:
- Discovering non-obvious codebase patterns
- Finding gotchas to avoid in the future
- Using better approaches than initially planned
- Revealing architectural insights

These learnings are saved to `.sublation-os/memory/` and become available to future implementations.

### Outputs

- Modified/created source code files
- Updated `tasks.md` with completed markers
- `verifications/final-verification.md` — verification report
- New learning entries in `.sublation-os/memory/`

### When to Use

After `tasks.md` is complete and ready for implementation

### Example Task Group Implementation

```
You: /implement-tasks
Agent: Which task group? (1, 2, or 3)

You: 1

Agent implements:
  ✓ 1.1 Write focused tests (created 5 tests)
  ✓ 1.2 Create database models (UserModel.ts)
  ✓ 1.3 Create migrations (migration_2025_11_09_auth.ts)
  ✓ 1.4 Set up associations (relationships in models)
  ✓ 1.5 Ensure tests pass (all 5 tests green)

Auto-learned: "Pattern found in UserRepository.cs:45
for handling null checks that applies to 3+ similar methods"
```

---

## Step 5: Learn — Capture Institutional Knowledge

**Command**: `/learn`

### What It Does

The `learn` command lets you manually capture insights, patterns, and lessons from your work session. While learning is also captured automatically during implementation (via the auto-learn skill), `/learn` allows you to manually capture insights that might not trigger auto-capture. All learnings are stored in `.sublation-os/memory/` and made available to future implementations.

### Learning Structure

Each entry follows this format:

```markdown
## Entry N — YYYY-MM-DD HH:mm

### Context
What happened? What was the task or problem?

### Lesson
The core principle or insight as a durable rule.

### Application
How should this affect future reasoning? Be specific and actionable.

### Example (Optional)
Concrete before/after or do/don't example.

### Tags
search, tags, for, discoverability
```

### Learning Categories

Store learnings in the appropriate category:

- **backend-lessons.md** — APIs, databases, services, server-side patterns
- **frontend-lessons.md** — UI components, state management, styling
- **testing-lessons.md** — Test strategies, frameworks, organization
- **architecture-lessons.md** — System design, patterns, project structure
- **general-lessons.md** — Workflow, tooling, debugging, misc

### Example Learning

```markdown
## Entry 3 — 2025-11-09 14:30

### Context
While implementing user authentication, discovered that UserRepository.cs
had null-checking logic duplicated in 3+ methods.

### Lesson
The UserRepository pattern includes explicit null-checks before
accessing related entities. This is deliberate for handling orphaned records.

### Application
When working with repository patterns in this codebase, always check
UserRepository.cs:45-60 for the null-handling pattern before writing
similar data access code.

### Example
// DO:
if (user != null && user.Profile != null) { ... }

// DON'T (will throw if user is deleted but referenced):
var profile = user.Profile;

### Tags
repository-pattern, null-handling, data-access, defensive-coding
```

### When to Use

- After discovering patterns that future implementations should know
- After fixing mistakes or debugging difficult issues
- After gaining architectural insights
- After learning codebase conventions (automatically captured during implementation)

---

## Step 6: Update-Standards-References — Maintain Consistency

**Command**: `/update-standards-references`

### What It Does

The `update-standards-references` command is a **maintenance tool** that ensures all agents in your project have access to:
- All standard files (coding style, API design, testing approach, etc.)
- All memory files (learnings and patterns captured in previous work)

This keeps your AI agents in sync with your team's standards and institutional knowledge. Agents that reference at least one standard or memory file are automatically updated to reference **all** of them:

```
.claude/agents/sublation-os/*.md — Updated with full references
.cursor/agents/sublation-os/*.md — Updated with full references (if using Cursor)
```

### Standards Included

- **Global**: Coding style, commenting, conventions, error handling, tech stack, validation
- **Backend**: API design, migrations, database models, query patterns
- **Frontend**: Accessibility, component structure, CSS approach, responsive design
- **Testing**: Test writing best practices and frameworks

### Memory Files Included

- `backend-lessons.md` — Server-side patterns and gotchas
- `frontend-lessons.md` — UI patterns and solutions
- `testing-lessons.md` — Testing approaches and strategies
- `architecture-lessons.md` — System design insights
- `general-lessons.md` — Workflow and tooling knowledge

### When to Use

- After creating new standards files
- After capturing multiple learnings
- After creating new agents
- Periodically as part of maintenance (monthly or quarterly)

### Result

After running this command, all your agents have access to:
- Every coding standard in your `.sublation-os/standards/` directory
- Every lesson captured in `.sublation-os/memory/`

This ensures consistent behavior and leverages accumulated knowledge across all AI-assisted work.

---

## The Complete Workflow in Action

Here's how a realistic feature development flows through all six steps:

### 1. Start with shape-spec

```
/shape-spec

Agent asks:
- What user roles need this feature?
- Do you have design mockups?
- How does this affect existing workflows?
- (3-4 more clarifying questions)

Output: planning/requirements.md
```

### 2. Write the specification

```
/write-spec

Agent:
- Analyzes requirements
- Searches codebase for reusable patterns
- Writes comprehensive spec.md
- References 4 existing components to reuse
- Specifies 3 new components to build

Output: spec.md
```

### 3. Break into tasks

```
/create-tasks

Agent:
- Creates Task Group 1 (Database Layer)
- Creates Task Group 2 (API Layer, depends on Group 1)
- Creates Task Group 3 (Frontend, depends on Groups 1-2)
- Creates Task Group 4 (Testing)

Output: tasks.md with 32 sub-tasks total
```

### 4. Implement task groups

```
/implement-tasks

You: Implement Task Group 1 (Database)
Agent: ✓ Creates models, migrations, associations
       Auto-learns: Pattern found in 3+ repository methods

You: Implement Task Group 2 (API)
Agent: ✓ Creates endpoints, validation, error handling
       Auto-learns: Consistent error response format

You: Implement Task Group 3 (Frontend)
Agent: ✓ Creates components, styling, state management
       Opens browser and tests as user

Output: complete feature, marked tasks, learnings captured
```

### 5. Capture additional learnings

```
/learn

You recognize a gotcha: "Always check for circular dependencies
in this specific import pattern"

Output: Entry added to general-lessons.md
```

### 6. Update agent standards

```
/update-standards-references

Updates all agents with references to:
- 20 standards files (API, testing, CSS, etc.)
- 5 memory files (lessons from this and past work)

Output: All agents now aware of new learnings
```

---

## Tips for Success

### Shape-Spec Phase
- Provide visual mockups if the feature has a UI
- Be detailed in your initial description
- Ask yourself: "Are there similar features already?"

### Spec-Writing Phase
- Trust the agent's codebase analysis
- Reuse components whenever possible
- Out of Scope prevents scope creep

### Task Creation Phase
- Review the task groups for logical ordering
- Ensure dependencies are clear
- Adjust task scope if groups are too large

### Implementation Phase
- Implement one task group at a time
- Run focused tests for each group
- Don't implement all at once (allows learning between groups)

### Learning Phase
- Capture patterns, not just fixes
- Be specific: Reference file names and line numbers
- Tag for discoverability

### Standards Maintenance
- Run `/update-standards-references` monthly
- Review memory files to see what you've learned
- Update standards when patterns repeat across projects

---

## Key Artifacts

By the end of this workflow, you have:

```
.sublation-os/specs/YYYY-MM-DD-feature-name/
├── spec.md                    ← Specification document
├── tasks.md                   ← Implementation tasks (all checked)
├── planning/
│   ├── initialization.md      ← Raw idea
│   ├── requirements.md        ← Gathered requirements
│   └── visuals/
│       ├── mockup.png
│       └── wireframe.jpg
└── verifications/
    └── final-verification.md  ← Verification report

.sublation-os/memory/
├── backend-lessons.md         ← New patterns captured
├── frontend-lessons.md        ← New patterns captured
└── (other lesson files updated with new entries)

Source code
├── models/                    ← New database models
├── services/                  ← New API layer
├── components/                ← New UI components
└── tests/                     ← New test files
```

---

## What Makes This Different

Traditional feature development:
```
Idea → (vague requirements) → Code → Bugs → Ship → Repeat
```

Sublation-OS workflow:
```
Idea → Shaped Requirements → Specification → Tasks →
Verified Implementation → Learned Lessons →
Better Future Work
```

Key differences:

1. **Requirements are researched, not guessed** — Spec-shaper asks hard questions
2. **Design is documented before coding** — Spec prevents rework
3. **Code is organized into focused tasks** — Each task group is testable
4. **Implementation is AI-assisted** — Faster, more consistent
5. **Learnings are captured** — Future work benefits from past experience
6. **Standards stay consistent** — Agents have access to all knowledge

This creates a virtuous cycle: each feature makes your team smarter for the next feature.

---

## Getting Started

1. **Have a feature idea?** Start with `/shape-spec`
2. **Need to integrate new standards?** Run `/update-standards-references`
3. **Want to review captured learnings?** Check `.sublation-os/memory/index.md`
4. **Need to understand an existing spec?** Read `.sublation-os/specs/YYYY-MM-DD-name/spec.md`

The workflow is designed to be flexible — you can run steps independently or as a complete pipeline, depending on your needs.