---
title: context engineering
---

## core idea

**Context engineering:** not what you tell the model, but what information you feed it. Manage the context window so the model accesses only high-signal data.

---

## the constraint

- **Context is finite** – recall accuracy drops as context grows ("context rot").
- **Attention is scarce** – transformers scale quadratically with token count (n²). Long contexts dilute focus.
- **Maximize quality per token** – the smallest set of high-signal tokens wins.

---

## principles

**System Prompts:** Use clear, minimal, structured language (e.g. `<background>`, `<instructions>`). Avoid brittle logic and vague goals.

**Tools:** Keep toolsets small, distinct, and token-efficient. Each tool should have one unambiguous purpose.

**Examples:** Prefer a few diverse, canonical examples over exhaustive edge cases.

**Message History:** Keep informative but tight; drop redundant or irrelevant exchanges.

---

## runtime context strategies

### 1. just-in-time retrieval

Load only what's needed at runtime via tools. Retrieve instead of memorize. Scales reasoning without bloating context.

### 2. hybrid retrieval

Combine preloaded static data + runtime exploration. Example: Claude Code reads `CLAUDE.md` upfront, then queries files dynamically.

### 3. decision coherence in multi-agent systems

Share full decision traces, not just messages. Prefer single-threaded agents with efficient retrieval over parallel agents with fragmented context. See [[Multi-Agent Pitfalls]].

---

## long-horizon techniques

**Compaction:** Summarize + restart context with condensed info; drop old tool outputs. Best for maintaining conversation continuity.

**Structured Note-Taking (Memory):** Persist notes outside context window (e.g. `NOTES.md`). Reload later for coherence. Best for iterative or long-term projects.

**Sub-Agent Architecture:** Split work into specialized agents with clean windows; main agent aggregates summaries. Best for complex, parallelizable research or code tasks.

---

## engineering takeaways

- Treat context as a budget — every token earns its keep.
- Build tools and prompts for efficiency, not verbosity.
- Use compaction + memory to stay coherent over long tasks.
- Prefer retrieval on demand to static context stuffing.
- Start simple; iterate on failure modes.

---

## tl;dr

Context engineering: decide what the model should know right now.

Best agents don't have the biggest contexts. They have the best-curated ones.

## reference
[Anthropic. (2025, September 29). *Effective context engineering for AI agents.*](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)

## related

- [[Why Claude Code vs Other Agents]] – implementation patterns across AI tools
- [[Sublation-OS as Applied Context Engineering]] – practical application in development
- [[Multi-Agent Pitfalls]] – coordination challenges in multi-agent systems
