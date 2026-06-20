---
title: AI System Prompt vs Memory
tags:
  - ai
  - ai-fundamentals
  - llm
aliases:
  - Claude Memory vs CLAUDE.md
---

# AI System Prompt vs Memory

Most frontier AI models (Claude, GPT, Gemini, etc.) separate two distinct persistence mechanisms: **system instructions** and **memory**. Understanding the difference helps you work with any AI assistant more effectively.

## The Core Distinction

**System instructions** are for *rules* — things the AI should always do or never do, regardless of conversation. They are imperative and behavioral.

**Memory** is for *facts* — things the AI learned during conversations that give context about the user, the project, or their preferences.

> [!tip] One-liner
> System instructions tell the AI **how to behave**; memory tells the AI **who it's working with and why**.

---

## System Instructions — Standing Orders

Called `CLAUDE.md` in Claude Code, `system prompt` in most APIs, `Custom Instructions` in ChatGPT.

Examples of what belongs here:
- "Use `pymupdf4llm` for PDF conversion"
- "Always write tests before implementation"
- "The main branch is `main`, not `master`"
- "Don't use MCP for Obsidian — use the CLI skill"
- "Always confirm before git push"

The AI follows these without being asked, in every conversation.

---

## Memory — Learned Context

Called `memory files` in Claude Code, `memories` in ChatGPT, `grounding context` in some systems.

Examples of what belongs here:
- "User is a data scientist"
- "Daily note system uses this specific format"
- "User prefers the CLI approach over MCP"
- "The main project is in a growth phase"

The AI recalls these to make better judgments, tailoring responses to who you are and what you're doing.

---

## Quick Reference Table

| Belongs in System Instructions | Belongs in Memory |
|---|---|
| Tool or workflow preferences | Who the user is, their role and background |
| Output format rules | What project they're working on and why |
| Coding conventions | Current priorities and context |
| Confirmation requirements | Domain knowledge the AI should assume |

---

## Context Window Impact

Neither system instructions nor memory are loaded per message — both are loaded **once at conversation start** and stay resident for the entire session.

```
┌─────────────────────────────────────────────┐
│ Context Window                              │
│ [System Instructions]  ← fixed, always here│
│ [Injected Memory]      ← loaded at start   │
│ [Message 1]                                 │
│ [Message 2]            ← grows over time   │
│ [Message 3]                                 │
└─────────────────────────────────────────────┘
```

| | System Instructions | Memory |
|---|---|---|
| When loaded | Conversation start | Conversation start (selectively in smart systems) |
| Grows during conversation? | No | No |
| **What actually grows** | **Conversation history — every exchange adds tokens** |

**Smart vs dumb memory systems:**
- *Dumb* (early ChatGPT): dumps all memories into system prompt upfront — fixed cost regardless of relevance
- *Smart* (Claude Code, newer GPT): keeps a lightweight index always loaded, pulls full memory files only when relevant

---

## Prompt Caching & When to Start a New Session

### How caching works

When you send a message, the AI doesn't reprocess everything from scratch. It caches the **processed prefix** (system instructions + memory + conversation so far) and only processes the new tokens added.

```
New session:     [~20K tokens: instructions + memory]  ← processed fresh, full cost
Follow-up msg:   [~20K cached prefix] + [new message]  ← prefix reused, only new tokens billed
```

Claude's cache TTL is **5 minutes**. If you send a message within 5 minutes of the last one, the prefix is warm and you pay only for new tokens. After 5 minutes, the cache is cold and the prefix is reprocessed.

### The real tradeoff

| | New Session | Continue Session |
|---|---|---|
| Upfront cost | ~20K tokens (fresh load) | Near zero (cache hit) |
| Per-message cost | Low (clean history) | Grows as history accumulates |
| Context quality | Clean, no noise | Carries all prior context (good and bad) |
| Cache state | Always cold at start | Warm within 5-min windows |

### When to start a new session

**Start fresh when:**
- Switching to a genuinely different task — old conversation history is noise, not signal
- The session has grown very long (history cost > 20K overhead of a fresh start)
- You're resuming after a long break — cache is cold anyway, so no caching benefit to continuing
- The AI seems to be "anchored" to earlier context and giving worse answers

**Stay in the same session when:**
- You're building on prior context (same task, same thread of thought)
- You're actively working within 5-minute windows — cache stays warm
- The conversation history is short and still relevant

> [!tip] Practical rule
> Same task = stay. Different task = new session. Long break (>5 min idle) = cache is cold anyway, so the penalty of starting fresh is just the one-time 20K load, not an ongoing cost.

### What happens after 5 minutes of idle

The cache expires and the **entire context is reprocessed from scratch** — but the conversation history is still there. This is the hidden cost of resuming a long idle session.

```
Short session, cold cache:
  20K (instructions + memory) + 2K (short history) = 22K tokens

Long session, cold cache:
  20K (instructions + memory) + 50K (long history) = 70K tokens
```

Resuming a long idle session can cost **more than starting fresh**. A new session is always ~20K. Resuming adds all accumulated history on top.

> [!warning] The irony
> The longer and more valuable your conversation history, the more expensive it becomes to resume after going idle.

**Revised decision rule:**

| Situation | What to do |
|---|---|
| Active work, same task | Stay — cache is warm, follow-ups are cheap |
| Long break + same task + short history | Fine to resume |
| Long break + same task + long history | Consider starting fresh |
| Long break + different task | Always start fresh |

### Auto-compaction

Claude Code automatically compacts long conversations when context gets large — summarizing older exchanges so history stays compact even across cache misses. This is the main mitigation against the "long idle session" cost problem.

---

## Vault-Level Memory

Memory relevant to a specific workspace can also live within that workspace (e.g. in an Obsidian vault) so it is searchable and linkable — not just hidden in the AI tool's internal storage.

---

## How Different Tools Implement This

| Concept | Claude Code | ChatGPT | Gemini |
|---|---|---|---|
| System instructions | `CLAUDE.md` | Custom Instructions | System Instructions |
| Persistent memory | `.claude/memory/` files | Memories | Gems (partial) |
| Scope | Per-project or global | Account-wide | Per-gem |
