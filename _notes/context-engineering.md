---
title: Context engineering
---

# Context Engineering

## Core Idea
**Context engineering** is the evolution of prompt engineering:  
it’s not just *what you tell the model*, but *what information you feed it* — managing the limited context window so the model has the highest-value data to reason over.

---

## Why It Matters
- **Context = finite resource** – as context size grows, recall accuracy drops (“context rot”).  
- **Attention = scarce** – transformers scale quadratically with token count (n²); long contexts dilute focus.  
- **Goal** – maximize outcome quality per token: the smallest set of *high-signal* tokens wins.

---

## Principles of Good Context Engineering

| Component | Guidance |
|------------|-----------|
| **System Prompts** | Use clear, minimal, structured language (e.g. `<background>`, `<instructions>`). Avoid brittle logic and vague goals. |
| **Tools** | Keep toolsets small, distinct, and token-efficient. Each tool should have one unambiguous purpose. |
| **Examples** | Prefer a few diverse, canonical examples over exhaustive edge cases. |
| **Message History** | Keep informative but tight; drop redundant or irrelevant exchanges. |

---

## Runtime Context Strategies

### 1. Just-in-Time Retrieval
- Load only what's needed at runtime via tools (file paths, queries, URLs).
- Mirrors human cognition: retrieve instead of memorize.
- Enables scalable reasoning without bloating context.

### 2. Hybrid Retrieval
- Combine preloaded static data + runtime exploration.
  Example: *Claude Code* reads `CLAUDE.md` upfront, then queries files dynamically.
- Balances speed and adaptability.

### 3. Decision Coherence in Multi-Agent Systems
- If using multiple agents, share full decision traces, not just messages
- Prefer single-threaded agents with efficient retrieval over parallel agents with fragmented context
- See [[Multi-Agent Pitfalls]] for detailed analysis of coordination challenges

---

## Long-Horizon Techniques

| Technique | What It Does | Best For |
|------------|---------------|----------|
| **Compaction** | Summarize + restart context with condensed info; drop old tool outputs. | Maintaining conversation continuity. |
| **Structured Note-Taking (Memory)** | Persist notes outside context window (e.g. `NOTES.md`). Reload later for coherence. | Iterative or long-term projects. |
| **Sub-Agent Architecture** | Split work into specialized agents with clean windows; main agent aggregates summaries. | Complex, parallelizable research or code tasks. |

---

## Engineering Takeaways
1. Treat **context as a budget** — every token must earn its keep.  
2. Build **tools and prompts for efficiency**, not verbosity.  
3. Use **compaction + memory** to stay coherent over long tasks.  
4. Prefer **retrieval on demand** to static context stuffing.  
5. Start simple; iterate based on observed failure modes.

---

## TL;DR
> **Context engineering = the discipline of deciding what the model should know right now.**

The best agents aren’t the ones with the biggest contexts,  
but the ones with the **best-curated ones**.

## Reference
[Anthropic. (2025, September 29). *Effective context engineering for AI agents.*](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)

## Related
- [[Why Claude Code vs Other Agents]] - How different AI coding tools implement (or ignore) context engineering
- [[Sublation-OS as Applied Context Engineering]] - Practical implementation of these principles for AI-assisted development
- [[Multi-Agent Pitfalls]] - Critical considerations for multi-agent architectures and decision coherence
