---
title: Article Writing Guidelines — Sublation Aesthetic
---

# Article Writing Guidelines

Style principles for writing technical documentation in the Sublation aesthetic: precise, minimal, system-like.

---

## Core Principles

### 1. Precision Over Persuasion

Delete every phrase that sounds like selling.

**Don't:**
> This process is designed to help teams work more efficiently.

**Do:**
> This process defines a repeatable loop for feature development.

The tone is **inevitable, not inspiring**. Confident because it doesn't need to explain itself.

---

### 2. Compress Explanations into Single Clauses

Corporate writing explains the "why" at length. Technical writing implies the why through clean structure.

**Don't:**
> This step ensures that you have a clear understanding of what you're building before you begin.

**Do:**
> Clarify what you're building before design begins.

Every sentence should feel **executable** — something that could almost run in a shell.

---

### 3. Use Declarative Fragments

Replace full sentences with declarative phrases. Reads like configuration.

**Don't:**
> The /write-spec command transforms your gathered requirements into a detailed specification document that developers can use to guide implementation.

**Do:**
> /write-spec turns requirements into a build plan.

**Same meaning, 60% shorter, infinitely sharper.**

---

### 4. Reduce Syntactic Decoration

Drop filler connectives: that, which, ensures that, so that, etc.
Turn multi-clause sentences into short, parallel statements.

**Don't:**
> The /write-spec command transforms your gathered requirements into a detailed specification document that developers can use to guide implementation.

**Do:**
> /write-spec turns requirements into a build plan.

---

### 5. Adopt Sparse, Slightly Detached Tone

Use neutral voice or imperative form — not cold, but machine-like.

**Don't:**
> You can use this command to...

**Do:**
> Use this command to...

**Or:**
> Command: /shape-spec — Gathers requirements through directed questioning.

Feels like system documentation, not onboarding copy.

---

### 6. Embrace Repetition When It Serves Rhythm

Avoid repeating key words in corporate writing. Anchor on them in minimalist writing.

Example — each step begins with action verb:

- /shape-spec **clarifies**
- /write-spec **formalizes**
- /create-tasks **structures**
- /implement-tasks **executes**
- /learn **distills**
- Maintain **synchronizes**

Reads like a command index — rhythmic and mechanical, almost poetic.

---

### 7. Cut Transitional Clutter

Drop "first," "next," "finally," "at this stage," "in this step."
Readers infer sequence from numbering. Replace with visual minimalism — clear headers, no narrative glue.

**Don't:**
> First, initialize the spec folder. Next, ask clarifying questions. Finally, refine if gaps are found.

**Do:**
```
1. Initialize spec folder
2. Ask clarifying questions
3. Refine if gaps found
```

---

### 8. Use Typographic Hierarchy, Not Verbal Emphasis

Let whitespace and typography carry structure instead of sentences like "In summary," "To conclude," etc.

**Don't:**
> In summary, the key takeaway is that...

**Do:**
> (Let headers and whitespace speak)

Example structure:
```
---
## Step 4 — /implement-tasks
Execute and verify task groups.
---

**Input:** tasks.md, spec.md
**Output:** Code, verifications, learnings

### Process

1. Select task group(s)
2. Build
3. Verify
```

---

### 9. Inject Low-Level Engineering Vocabulary

Swap "leverages," "ensures," and "collaborates" with verbs that sound like processes.

**Better verbs:**
- parse (instead of "gather")
- map (instead of "organize")
- resolve (instead of "handle")
- generate (instead of "create")
- verify (instead of "check")
- sync (instead of "keep in sync")

They imply computation — which fits technical documentation.

---

### 10. End With Recursion, Not Inspiration

Corporate docs end with "Key takeaways."
Technical documentation ends with loops.

**Don't:**
> This creates a virtuous cycle: each feature makes your team smarter for the next feature.

**Do:**
> The loop closes when knowledge becomes reference.
> Every new feature redefines the system that builds it.

Minimalist and philosophical.

---

### 11. Use Lowercase Headings

Avoid title case. Headings feel machine-like when left lowercase.

**Don't:**
> ## Avoid Writing Like This

**Do:**
> ## Avoid writing like this

Reads like configuration, not marketing. Preserves minimalist visual rhythm.

---

## Structural Pattern

Use this pattern for reference articles (especially procedural content):

```markdown
## Step X: /command
One-line purpose.

**Input:** ...
**Output:** ...
**Use when:** ...

### Process / Generates / Categories
(2–3 subsections, bullets only)

### Example
(Minimal, code-focused)
```

---

## Quick Reference: Before/After

### Example 1: Descriptive Paragraph

**Before:**
> The shape-spec command orchestrates a three-phase requirement-gathering process that ensures you have a clear, comprehensive understanding of what you're building before you start designing it.

**After:**
> /shape-spec gathers requirements through three phases: initialize, question, refine. Clarity before design.

---

### Example 2: Explanation Section

**Before:**
> The /implement-tasks command oversees the actual implementation of one or more task groups, running code verification and automatically capturing learnings.

**After:**
> /implement-tasks executes task groups. Implements, tests, records insight.

---

### Example 3: Closing Statement

**Before:**
> This creates a virtuous cycle: each feature makes your team smarter for the next feature.

**After:**
> The loop closes when knowledge becomes reference.
> Every feature feeds the next.
> The system learns itself.

---

## Table Formatting

Keep tables minimal. Use them for reference, not explanation.

**Good:**
```
| Step | Input | Output | Resolves |
|------|-------|--------|----------|
| `/shape-spec` | Idea | requirements.md | Ambiguity |
| `/write-spec` | Requirements | spec.md | Redundancy |
```

**Bad (too much explanation in cells):**
```
| Step | What It Does | Why You Need It |
|------|--------------|-----------------|
| `/shape-spec` | Clarifies the problem with targeted questions and visual assets | Ensures you're building the right thing |
```

---

## Checklist for Article Review

- [ ] No persuasive language ("designed to," "ensures," "helps you")
- [ ] Sentences compress to single clauses or fragments
- [ ] No filler connectives (that, which, ensures that, so that)
- [ ] Imperative voice where appropriate ("Do X," not "You can do X")
- [ ] Engineering vocabulary (parse, map, resolve, verify, sync)
- [ ] No transitional clutter (first, next, finally, in summary)
- [ ] Whitespace and typography carry structure
- [ ] Ends with recursion or system insight, not motivation
- [ ] Tables are minimal and reference-focused
- [ ] Repetition of key words creates rhythm
- [ ] Headings use lowercase, not title case

---

## Tone Reference

| Avoid | Adopt |
|-------|-------|
| "designed to help" | "defines," "structures," "enables" |
| "ensures that" | "verifies," "checks" |
| "leverages" | "uses," "parses," "maps" |
| "collaborates with" | "integrates with," "syncs with" |
| "You can use this to..." | "Use this to...", "Command: ..." |
| "In summary" | (Let whitespace speak) |
| "Key takeaway" | (Recursive insight) |

---

## Examples in Context

### Full Article Section: Before

```markdown
## The Shape-Spec Step

The shape-spec command is designed to help you gather requirements
before you start designing anything. It ensures that you have a clear
understanding of what you're building by asking clarifying questions.

The process has three phases. First, it initializes a spec folder
where all artifacts live. Next, it asks you 4–8 clarifying questions
about your feature, including things like user roles, design mockups,
and technical constraints. Finally, if there are gaps, the agent asks
follow-up questions to fill them in.

When you should use this step: when starting a new feature, adding a
significant capability, or any work that takes 4+ hours to implement.
```

### Full Article Section: After

```markdown
## Step 1: /shape-spec
Clarify before design.

**Input:** Raw idea
**Output:** requirements.md
**Use when:** Starting new feature, significant scope (4+ hours)

### Process

1. Initialize spec folder (`.sublation-os/specs/YYYY-MM-DD-feature-name/`)
2. Parse requirements via 4–8 clarifying questions:
   - Integration with existing functionality
   - User stories and use cases
   - Visual design assets (mockups required)
   - Technical constraints
   - Reusable code in codebase
3. Refine if gaps found

### Result

`requirements.md` with answers, visual references, ready for specification.
```

---

## References

- Minimalist technical writing (inspired by system documentation and CLI help)
- Engineering-focused vocabulary (computation, not motivation)
- Recursion and loops as philosophical closure (not inspirational clichés)
