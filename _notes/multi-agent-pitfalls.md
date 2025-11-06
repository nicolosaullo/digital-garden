---
title: Multi-Agent Pitfalls
---

# Multi-Agent Pitfalls

Analysis based on Walden Yan's "Don't Build Multi-Agents" (Cognition AI, 2025)

## The Core Problem

Multi-agent architectures create fragile systems that struggle with reliability in production. The fundamental issue is **decision coherence**: parallel agents operating independently generate incompatible outputs due to unstated assumptions.

## Two Principles for Agent Architecture

Yan presents two core principles:

### Principle 1: Share Context, Share Full Traces

"Share context, and share full agent traces, not just individual messages"

**Why**: Agents need to understand not just what was done, but why it was done and what alternatives were considered. Passing only individual messages loses critical decision context.

### Principle 2: Avoid Conflicting Decisions

"Actions carry implicit decisions, and conflicting decisions carry bad results"

**Why**: Every action an agent takes carries implicit decisions. When agents work in parallel without sharing decision context, they make conflicting implicit choices that cannot be reconciled later.

## The Flappy Bird Example

Yan illustrates the problem with a game development scenario:

The task is divided into subtasks for parallel execution:
- Subtask 1 produces a Super Mario Bros-style background instead of Flappy Bird pipes
- Subtask 2 creates a bird that doesn't match the game's mechanics

**Problem**: The final agent struggles to combine these incompatible outputs because the subtask requirements weren't communicated properly. Parallel subagents lacked visibility into each other's work, creating conflicting assumptions about visual style, mechanics, and design decisions.

### Why This Happens

When agents work in parallel:
- Agent A makes implicit assumptions about the overall aesthetic
- Agent B makes different implicit assumptions
- Neither communicates these unstated decisions
- The integration agent cannot reconcile contradictory results

### Generalizing Beyond Games

This same pattern occurs in software development. For example (illustrative scenario, not from source):
- Agent A implements one approach
- Agent B assumes a different approach
- Integration fails due to incompatible assumptions

## Criticism of Existing Tools

Yan specifically criticizes:
- **OpenAI Swarm** (github.com/openai/swarm)
- **Microsoft AutoGen** (github.com/microsoft/autogen)

These tools "actively push concepts which I believe to be the wrong way of building agents" through multi-agent architectures.

## Recommended Approaches

Yan recommends three alternatives to multi-agent systems:

### 1. Single-Threaded Linear Agents

Maintain continuous context through a single agent execution path:
- Sequential task execution
- Unbroken decision history
- No coordination overhead
- Natural context accumulation

**Advantage**: Ensures coherence without fragmentation

### 2. Compression Models for Long-Duration Tasks

When context becomes too long:
- Use an LLM to summarize conversation history
- Compress into key decisions and events
- Preserve decision threads
- Maintain continuity without splitting context

**Use case**: Addresses context window overflow while maintaining single decision thread

### 3. Limited Subagents

Use subagents only for:
- Answering isolated questions
- Information retrieval
- Research tasks

**Never** use parallel subagents for:
- Writing code simultaneously
- Making design decisions independently
- Creating interdependent artifacts

**Example**: Subagents can answer questions about codebases, but should not perform parallel implementation work.

### 4. Single-Model Edit Decisions

Avoid separating edit decisions from edit application across different models or agents.

## Timeline and Caveats

**Current State (2025)**: "Running multiple agents in collaboration only results in fragile systems"

**Future Outlook**: Yan expects improved agent-to-agent collaboration "as we make our single-threaded agents even better," but multi-agent coordination is not production-ready now.

## Implications for Context Engineering

This perspective complements [[context-engineering]] principles:

**Context efficiency principle**: Minimize context, load only what's needed

**Decision coherence principle**: If splitting context across agents, you MUST share full decision traces, not just final outputs

These aren't contradictory - they're complementary:
- Engineer context to be minimal but complete
- Prefer single agent with efficient retrieval
- If using subagents, share full context and traces

## How Sublation-OS Handles This

[[Sublation-OS as Applied Context Engineering]] implements Yan's recommendations:

**Aligned with recommendations:**
- Subagents receive full specifications, not just tasks
- Standards and memory provide shared decision context
- Agents are specialized but sequential, not parallel
- Main workflow: plan → implement → verify (phases, not parallel work)

**Example**: The implementer agent receives:
- Complete spec with requirements and context
- Relevant standards (shared conventions)
- Related learnings (past decisions)

**Anti-pattern avoided**: Never splitting implementation across parallel agents making independent architectural decisions.

## Practical Guidelines

### Red Flags (What to Avoid)
- "Let's split this feature across 3 agents working in parallel"
- "Agent A will handle backend, Agent B will handle frontend" (simultaneously)
- "Each agent can decide its own approach"
- Passing only final outputs between agents

### Green Flags (Recommended Patterns)
- "Let's use a subagent to research this API before implementing"
- "Agent completes backend, then frontend agent gets full context"
- "All agents follow the same standards and see the same decisions"
- Sharing complete reasoning traces between agents

## Key Takeaway

Multi-agent systems require:
1. Full context sharing (decision traces, not messages)
2. Sequential execution or explicit coordination
3. Shared knowledge base (standards, conventions, past decisions)
4. Single source of truth for architectural choices

Without these, you get fragile systems with conflicting implicit decisions.

**Current best practice (2025)**: Single agent with efficient context engineering beats multiple agents with fragmented context.

## References

Yan, W. (2025). "Don't Build Multi-Agents." Cognition AI. https://cognition.ai/blog/dont-build-multi-agents

## Related

- [[context-engineering]] - Core context management principles
- [[Why Claude Code vs Other Agents]] - How Claude Code avoids multi-agent pitfalls
- [[Sublation-OS as Applied Context Engineering]] - Sequential agent architecture implementation
