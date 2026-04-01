---
title: What is a Hook?
parent: AI Fundamentals
permalink: /ai-fundamentals/what-is-a-hook/
---

# Hooks
Hooks are user-defined shell commands that execute at specific points in Claude Code’s lifecycle. They are configured in `settings.json` — not in memory or preferences — because hooks are executed by the Claude Code harness itself, not by the AI.

Hooks are automated injections triggered on defined events. For example, before making a tool call, after writing a document, etc. Hooks are used for: 
- Deterministic actions: Always perform an action when something or some work is completed. For example, run tests on code commit, or run a security scan before submitting the pr
- workflow actions: Connect multiple actions in a workflow using hooks. For example, send a Google chat notification once PR-reviewer has completed the review.
- guardrails - check before a tool call that no harmful, dangerous action is going to happen. 

## Common Hook Events

| Event                | When it Fires                                              | Typical Use Case                                                                   |
| :------------------- | :--------------------------------------------------------- | :--------------------------------------------------------------------------------- |
| **SessionStart**     | When you first launch the assistant.                       | **Setup**: Pulling the latest Jira tickets or bug reports to prime the AI.         |
| **UserPromptSubmit** | Immediately after you hit enter on a prompt.               | **Context**: Injecting the current time or recent git status into the prompt.      |
| **PreToolUse**       | Before the AI runs any tool (e.g., `bash`, `write_file`).  | **Blocking**: Checking for hardcoded secrets before saving.                        |
| **PostToolUse**      | After a tool call succeeds.                                | **Cleanup**: Auto-formatting code with Prettier/Black after an edit.               |
| **Notification**     | When the AI needs your attention (e.g., for a permission). | **Alerts**: Sending a desktop notification so you can switch back to the terminal. |
| **Stop**             | When the agent finishes responding.                        | **Alerts**: Notify you (desktop/chat) that Claude is done and needs your attention. |
