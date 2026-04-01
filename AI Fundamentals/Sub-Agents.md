---
title: Sub-Agents
parent: AI Fundamentals
permalink: /ai-fundamentals/sub-agents/
---

# Sub-Agents
Agents defined in `.cursor/agents` or `.claude/agents` are sub-agents that run like a forked child process with their own isolated execution context.

> A sub-agent is an AI specialist that can independently do its job in isolation, provided it's given the context and tool access it needs.

**Important:** Sub-agents start with a **clean slate** — they do NOT automatically inherit the parent conversation history. The parent agent must **explicitly pass** relevant context (task description, file paths, constraints, prior findings) when spawning the sub-agent. What it doesn't receive, it doesn't know.

Agent names follow persona-driven naming such as `pr-reviewer.md`, `security-auditor.md`, etc.