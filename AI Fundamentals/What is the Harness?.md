---
title: What is the Harness?
parent: AI Fundamentals
permalink: /ai-fundamentals/what-is-the-harness/
---

# What is the Harness?

The **harness** is the outer shell — the Claude Code CLI application running on your machine. It has no intelligence of its own. It is deterministic software (if/then logic, event listeners, process management) that **manages, controls, and enables** the AI agent.

> Analogy: A harness on a horse — it's not the horse, but it controls and directs it.

## What the Harness Does
- Starts up and manages the conversation loop
- Reads config and `settings.json`
- Fires **hooks** at lifecycle events
- **Executes tools** on behalf of the LLM (bash, file read/write, etc.)
- Handles permissions
- Sends prompts to the LLM and routes responses back to you

The LLM never directly touches your filesystem or runs commands. It *requests* actions — the harness *executes* them.

---

## Harness vs. AI Agent vs. LLM

These three are often conflated. They are distinct:

| | **LLM** | **AI Agent** | **Harness** |
|---|---|---|---|
| What it is | The brain | The system around the brain | The environment the system runs in |
| Reasons? | ✅ Yes — this is the LLM's job | ❌ No — it orchestrates the LLM | ❌ No — pure deterministic software |
| Executes tools? | ❌ No | ❌ No — it requests tool calls | ✅ Yes — actually runs them |
| Has memory? | ❌ Not between calls | ✅ Via memory modules | ✅ Via config files |
| Fires hooks? | ❌ No | ❌ No | ✅ Yes |

> **Key insight:** When people say *"the agent reasons"* — that's shorthand. The **LLM** reasons. The **agent** feeds context to the LLM and acts on the result. The **harness** executes whatever action the agent requests.

---

## How They Work Together (Example)

```
You type a prompt
        │
        ▼
   HARNESS fires UserPromptSubmit hook
   (injects git status, timestamp, etc.)
        │
        ▼
   HARNESS sends enriched prompt to the AGENT
        │
        ▼
   AGENT feeds context + memory to the LLM
        │
        ▼
   LLM reasons → decides to call the Write tool
        │
        ▼
   HARNESS fires PreToolUse hook (checks for secrets)
        │
        ▼
   HARNESS executes the file write
        │
        ▼
   HARNESS fires PostToolUse hook (runs Prettier)
        │
        ▼
   HARNESS returns result to the AGENT
        │
        ▼
   AGENT passes result back to the LLM for next reasoning step
```

---

## Why Hooks Live in `settings.json`, Not AI Memory

Because hooks are **executed by the harness**, not the AI. The AI can't enforce deterministic behavior — it might forget, or a new session resets its context. The harness reads `settings.json` every time and fires hooks mechanically, regardless of what the AI is doing.

---

## Analogy

| | Role |
|---|---|
| **LLM** | The surgeon — makes all the decisions |
| **AI Agent** | The surgical team — coordinates the procedure |
| **Harness** | The operating theatre — equipment, rules, instruments |
| **Tools** | The scalpel — surgeon asks for it; theatre provides it |
