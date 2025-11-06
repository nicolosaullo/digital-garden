---
title: Presentation Hooks - Context Engineering
---

# Presentation Hooks: Context Engineering & AI Agents

Collection of opening hooks for presentations on [[context-engineering]], [[multi-agent-pitfalls]], and [[why-claude-code]].

**Note**: These are communication frameworks designed to make research concepts accessible. All claims should be verified against the source articles before presentation use.

## The Problem-First Hook (Technical Audience)

**Opening:**

"Raise your hand if you've ever had this conversation with an AI coding assistant:

You: 'Remember, we use Redux for state management.'
AI: 'Got it, I'll use Redux.'

Next session, 5 minutes later:

You: 'Why did you implement this with Context API?'
AI: 'Oh, should I use Redux instead?'

Your AI assistant has amnesia. Every. Single. Session.

Imagine if your junior developer forgot your entire tech stack every morning. Yet we accept this from AI agents because we think it's inevitable.

It's not. The problem isn't the AI's memory - it's how we're engineering its context."

**Why it works**: Relatable pain point, provocative comparison, promises a solution

**Research basis**: Anthropic's context engineering research addresses persistent context across sessions

---

## The Failure Scenario Hook (Product/Design Audience)

**Opening:**

"Let me tell you about the time two AI agents built a Flappy Bird game together.

Agent A was assigned the background. It created a Super Mario Bros-style retro environment.

Agent B was assigned the bird character. It designed something that didn't match the game mechanics.

The final agent tried to combine them and... complete incompatibility. They looked like they belonged in different games. Because they did.

Here's what happened: Agent A made an implicit decision about aesthetic style. Agent B made a different implicit decision. Neither communicated. Neither was wrong. But together? Disaster.

This isn't a cute anecdote about game development. This exact problem is happening in production codebases right now. One agent assumes one architectural approach. Another agent assumes differently. Integration fails.

The multi-agent future everyone's excited about? It's more fragile than you think."

**Why it works**: Concrete story, visual imagery, relatable failure mode, stakes escalation

**Research basis**: Walden Yan's "Don't Build Multi-Agents" uses this exact example to illustrate decision coherence problems

---

## The Philosophical Hook (Academic/Research Audience)

**Opening:**

"In software development, we've spent decades optimizing for computational efficiency. We measure Big O complexity, we profile memory usage, we obsess over milliseconds.

But with AI agents, we've introduced a new scarce resource we barely understand how to measure: context.

Context is like RAM, but for reasoning. You have a finite context window. Every project convention, every code example, every instruction costs tokens. Fill it with noise, and the model can't think. Fill it with redundancy, and you waste capacity. Fragment it across multiple agents, and they make conflicting decisions.

The question isn't 'how do we build more powerful AI agents?' The question is: What should the model know right now?

This is context engineering. And it's the difference between AI agents that help you ship features, and AI agents that ship bugs."

**Why it works**: Reframes familiar concepts, introduces new mental model, poses provocative question

**Research basis**: Anthropic's framing of context as finite resource with n² attention scaling

---

## The Counterintuitive Hook (General Tech Audience)

**Opening:**

"Quick poll: Who here thinks the best AI coding assistant is the one with access to the most information?

Makes sense, right? More context = better decisions.

Here's the problem: Research shows that as context windows grow, LLM recall accuracy drops. It's called 'context rot' - model accuracy decreases as token count rises.

Your AI assistant doesn't have perfect memory. It has very good search with degradation at scale.

The best agents aren't the ones with the biggest context windows. They're the ones with the best-curated context windows.

Think about it: You don't memorize your entire codebase. You retrieve what you need, when you need it. Junior developers fail because they try to hold everything in their heads. Senior developers succeed because they know what to forget.

Your AI agent needs to learn the same lesson."

**Why it works**: Challenges assumptions, uses research findings, provides analogy to human cognition

**Research basis**: Anthropic's explicit discussion of context rot and diminishing returns

---

## The Architectural Hook (Engineering Leaders)

**Opening:**

"What if I told you that most AI coding agents are wasting the majority of their context window before they write a single line of code?

Here's what typically happens:
- Load lots of context upfront
- User asks a question
- Most of that loaded context is irrelevant to the actual question

Anthropic's research identifies this as the core challenge: context is a finite resource with diminishing returns as it grows.

The solution isn't bigger context windows. It's better context engineering: load minimal baseline, retrieve precisely what's needed, maintain coherent decision threads.

This isn't just about making AI agents smarter. It's about making them fundamentally more effective."

**Why it works**: Identifies waste, provides research-backed principle, promises efficiency

**Research basis**: Anthropic's core context engineering principles

---

## The Team Hook (Engineering Managers)

**Opening:**

"Your best senior developer leaves. Six months of context about why certain decisions were made, what patterns to avoid, which libraries caused problems - all gone.

You've experienced this, right? The knowledge walking out the door?

Now multiply that by every AI coding session. Because that's what's happening.

Every time you close your AI coding assistant, learned patterns, discovered gotchas, debugged edge cases... gone.

Next session, you're teaching the AI from scratch. Again.

But here's the thing: Unlike human developers, AI agents can have perfect institutional memory. If we architect for it.

What if your AI agent remembered every performance optimization discovered, every security vulnerability patched, every architectural decision and its rationale?

Not just remembered - actually applied them in every future session.

That's not science fiction. That's context engineering with persistent memory."

**Why it works**: Relatable pain point (knowledge loss), connects to management concerns, promises retention

**Research basis**: Anthropic's structured note-taking and memory techniques

---

## The Time-Travel Hook (Storytelling Approach)

**Opening:**

"Imagine you're a developer in 2030. You ask your AI agent to add user authentication to your app.

It doesn't ask what framework you're using. It already knows - it learned that when you set up the project.

It doesn't ask about your error handling conventions. They're documented in standards it references automatically.

It doesn't make the same JWT signing mistake the last developer made. That's captured in the team's memory system.

It just... implements authentication. Correctly. Following your patterns. Learning from past mistakes.

Now come back to 2025. Ask most AI assistants to add authentication. First thing it says: 'What framework are you using?'

The future isn't about more powerful models. It's about models with better memory. But not model memory - architectural memory. Context engineering memory.

And you can build this today."

**Why it works**: Paints vivid future, creates contrast with present, actionable

**Research basis**: Combines Anthropic's context engineering techniques with practical implementation

---

## The Research Translation Hook (Data-Driven Audience)

**Opening:**

"Anthropic published research in September 2025 on context engineering for AI agents. Three key findings:

One: Context rot is real. As context size grows, model recall accuracy drops. This isn't a limitation to overcome with bigger windows - it's an architectural constraint of how transformers work. n² pairwise relationships mean attention gets diluted.

Two: Just-in-time retrieval beats upfront loading. Maintaining lightweight identifiers and dynamically loading data mirrors how human cognition actually works.

Three: Sub-agent architectures work, but only with full context sharing. Parallel agents making independent decisions create fragile systems with conflicting assumptions.

These aren't theoretical observations. They're engineering principles derived from production systems.

The question is: How many teams are actually implementing these principles versus just throwing more context at the problem?"

**Why it works**: Leads with credible source, presents concrete findings, poses challenge

**Research basis**: Direct summary of Anthropic's published research

---

## Choosing Your Hook

**Use Problem-First** for: Technical conferences, developer meetups
**Use Failure Scenario** for: Product teams, cross-functional audiences
**Use Philosophical** for: Research presentations, academic settings
**Use Counterintuitive** for: General tech conferences, keynotes
**Use Architectural** for: Engineering leadership, technical strategy discussions
**Use Team** for: Engineering managers, CTOs, organizational talks
**Use Time-Travel** for: Futurist conferences, vision presentations
**Use Research Translation** for: Data science teams, evidence-based audiences

---

## Follow-Up Slides After Hook

After any hook, transition with:

"Today, I'm going to show you three things:

1. **Why context engineering is critical for AI-assisted development** - based on Anthropic's September 2025 research
2. **How multi-agent systems fail** - based on Cognition AI's analysis of production systems
3. **A practical framework** that implements these research findings

By the end, you'll understand why the future of AI coding isn't about better models - it's about better architecture."

## Important Note on Presentation Use

These hooks are designed to communicate complex research in accessible ways. Before using in presentations:

1. Read the source materials: Anthropic's context engineering article and Cognition's multi-agent analysis
2. Verify specific claims against sources
3. Adjust examples to match your audience's technical level
4. Cite sources appropriately

The goal is translating academic research into practical insights, not creating unsupported claims.

## Related

- [[context-engineering]] - Core concepts to present
- [[multi-agent-pitfalls]] - Key failure modes to explain
- [[why-claude-code]] - Tool architecture for context
- [[Sublation-OS as Applied Context Engineering]] - Practical implementation to showcase
