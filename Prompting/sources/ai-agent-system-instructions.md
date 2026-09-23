---
title: "Source: AI Agent System Instructions (Dust Blog + Claude Code Tutorial)"
---

Condensed extraction from two articles: the Dust Blog post *"How to Write AI Agent Instructions That Actually Work"* and the *Claude Code Agent Tutorial* ("How to Build an AI Agent with Claude Code"). Both cover the same underlying question: how to author persistent system instructions (`CLAUDE.md`, an agent builder's system prompt, etc.) rather than one-off prompts.

Distilled from `ai-agent-manuals-note.md` and `ai-agent-manuals-note-v2.md`, downloaded 2026-09-23.

## Core distinction: prompts vs. instructions

- **Prompts** are ephemeral and task-focused: one-time requests that end after a single turn, starting from scratch each session.
- **Instructions** are persistent and role-focused: they live in a standing config file and define "how you always operate" across hundreds of tasks and sessions.

**Three levels of AI interaction:**
1. Basic Chat — simple Q&A, a glorified search engine.
2. Builder Mode — one-off creations, but the human manages every micro-step.
3. Agentic Work — hand the agent a goal; it breaks it into phases, asks clarifying questions, executes sequentially, reviews its own work, and delivers a finished result.

> "The intelligence of an agent lies in the thoughtfulness of its instructions, not its technical tool stack."

## The three-layer mental model

- **Identity Layer** — professional role, domain stance, tone, audience context.
- **Decision Layer** — hard rules, confidence thresholds, clarification/escalation triggers.
- **Execution Layer** — step-by-step processes, explicit tool-trigger conditions, structured output templates.

## Six-part anatomy of a system instruction file

1. **Role, Expertise & Context** — who the agent is, technical stance, business context.
   - Weak: "You are a helpful assistant."
   - Strong: "You are a Senior Technical Product Specialist for a B2B SaaS platform. You prepare pre-sprint feature specifications and technical architecture briefs for senior engineering teams."
2. **Process & Step-by-Step Workflows** — numbered stages for complex multi-step tasks, to prevent disorganized execution, tool-calling errors, or skipped steps.
3. **Two non-negotiable operational rules:**
   - *Clarification before execution* — ask clarifying questions about scope, audience, and constraints before starting any complex task.
   - *Mandatory planning mode* — present a written execution plan and wait for explicit approval before touching files or running multi-step tasks.
4. **Tool Usage Guidelines** — when to use each tool, what inputs it needs, how to handle failures. Give tools descriptive, semantic names to improve selection accuracy.
5. **Output Format, Tone & File Conventions** — exact structural templates, word-count limits, formatting preferences (e.g. tables for comparisons), file-naming rules.
6. **Boundaries & Guardrails** — the three-tier framework below.

## Three-tier boundary framework

- ✅ **Always do** — require citations, present a plan and get confirmation, maintain transparent auditability.
- ⚠️ **Ask first** — before modifying database schemas or core architecture, introducing new third-party tools/libraries, or making external API calls.
- 🚫 **Never do** — never fabricate facts or metrics, never install unapproved dependencies, never pad outputs, never make unrequested rewrites.

## Related distilled notes

See [[../templates/system-instructions|System Instructions Template]] for the copy-paste skeleton built from this framework, and the Gemini user-level template filed there for a worked example of the Identity/Decision/Execution layers applied to a real personal setup.
