---
title: What is the Harness?
---

# What is the Harness?

The **harness** is the deterministic code around the model that controls its inputs, actions, and outputs. It has no intelligence of its own. It is deterministic software (if/then logic, event listeners, process management) that **manages, controls, and enables** the AI agent.

In Claude Code, the harness is the outer shell: the CLI application running on your machine. The rest of this note uses Claude Code as the example; see [Outside Claude Code](#outside-claude-code) for what the same idea looks like in a service you build.

> Analogy: A harness on a horse — it's not the horse, but it controls and directs it.

## What the Harness Does
- Starts up and manages the conversation loop
- Reads config and `settings.json`
- Fires **hooks** at lifecycle events
- **Executes tools** on behalf of the LLM (bash, file read/write, etc.)
- Handles permissions
- Sends prompts to the LLM and routes responses back to you

The LLM never directly touches your filesystem or runs commands. It *requests* actions — the harness *executes* them.

## Outside Claude Code

Hooks and permissions are Claude Code's names for these controls. In a service you build yourself (say, an agent that triages support tickets), the same job is done by:

| Claude Code | In your own service |
|---|---|
| Permissions | Which tools and data the agent is allowed to touch |
| Hooks | Validators that check each result, retries on failure |
| Tool execution | Your code calling the APIs the model asked for |
| Conversation loop | Routing code, including a fallback to a human queue |

A fixed output format usually comes from **structured output** at the model API, not from a hook. The harness then validates it.

If you build with an agent SDK, the agent loop and the harness are often the same code. The distinction still helps: the model decides, the code around it controls and executes.

## What the Harness Can't Do

The harness guarantees the **shape** of an answer, not whether it's **right**. A validator accepts "P2, Billing" and "P1, Outage" equally, because both are well-formed. Only a clear problem definition, an eval, and a human fallback tell you which one is correct.

- **Evals are separate from the harness.** The harness enforces rules on every request at runtime. An eval runs offline, against labelled examples, to measure how often the model gets it right. It measures; it doesn't enforce.
- **"Evaluation harness" means something else.** In ML, an evaluation harness (e.g. `lm-evaluation-harness`) is a test runner for evals. Same word, different thing.
- **"Deterministic" describes the harness's role, not every part.** A hook can call a model (e.g. an LLM-as-judge check), and then that step is no longer deterministic.

---

## Harness vs. AI Agent vs. LLM

These three are often conflated. They are distinct:

| | **LLM** | **AI Agent** | **Harness** |
|---|---|---|---|
| What it is | The brain | The system around the brain | The environment the system runs in |
| Reasons? | ✅ Yes: this is the LLM's job, including planning | ❌ No: it runs the loop and keeps the plan | ❌ No: deterministic software |
| Executes tools? | ❌ No | ❌ No — it requests tool calls | ✅ Yes — actually runs them |
| Has memory? | ❌ Not between calls | ✅ Via memory modules | ✅ Via config files |
| Fires hooks? | ❌ No | ❌ No | ✅ Yes |

> **Key insight:** When people say *"the agent reasons"* — that's shorthand. The **LLM** reasons. The **agent** feeds context to the LLM and acts on the result. The **harness** executes whatever action the agent requests.
>
> The same goes for planning. [[what-is-an-ai-agent|What is an AI Agent?]] lists Planning as one of an agent's modules. The plan itself is produced by the LLM; the agent stores it and works through it step by step.

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