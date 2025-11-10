---
title: context engineering
---

Not what you tell the model, but what information you feed it. Manage the context window so the model accesses only high-signal data.

## the constraint

- **context is finite** – recall accuracy drops as context grows ("context rot").
- **attention is scarce** – transformers scale quadratically with token count (n²). long contexts dilute focus.
- **maximize quality per token** – the smallest set of high-signal tokens wins.

## principles

**system prompts:** use clear, minimal, structured language (e.g. `<background>`, `<instructions>`). avoid brittle logic and vague goals.

**tools:** keep toolsets small, distinct, and token-efficient. each tool should have one unambiguous purpose.

**examples:** prefer a few diverse, canonical examples over exhaustive edge cases.

**message history:** keep informative but tight; drop redundant or irrelevant exchanges.

## runtime context strategies

### 1. just-in-time retrieval

load only what's needed at runtime via tools. retrieve instead of memorize. scales reasoning without bloating context.

### 2. hybrid retrieval

combine preloaded static data + runtime exploration. example: claude code reads `CLAUDE.md` upfront, then queries files dynamically.

### 3. decision coherence in multi-agent systems

share full decision traces, not just messages. prefer single-threaded agents with efficient retrieval over parallel agents with fragmented context. see [[Multi-Agent Pitfalls]].

## long-horizon techniques

**compaction:** summarize + restart context with condensed info; drop old tool outputs. best for maintaining conversation continuity.

**structured note-taking (memory):** persist notes outside context window (e.g. `NOTES.md`). reload later for coherence. best for iterative or long-term projects.

**sub-agent architecture:** split work into specialized agents with clean windows; main agent aggregates summaries. best for complex, parallelizable research or code tasks.

## engineering takeaways

- treat context as a budget — every token earns its keep.
- build tools and prompts for efficiency, not verbosity.
- use compaction + memory to stay coherent over long tasks.
- prefer retrieval on demand to static context stuffing.
- start simple; iterate on failure modes.

## related

- [[Why Claude Code vs Other Agents]] – implementation patterns across AI tools
- [[Sublation-OS as Applied Context Engineering]] – practical application in development
- [[Multi-Agent Pitfalls]] – coordination challenges in multi-agent systems
