---
title: Skills vs Agents
---

# Skills vs Agents
| **Feature** | **Skill (`SKILL.md`)**                                         | **Agent / Subagent (`.md`)**                                 |
| ----------- | -------------------------------------------------------------- | ------------------------------------------------------------ |
| Concept     | The "Manual": A specific playbook or set of instructions.      | The "Worker": An autonomous entity that performs a task.     |
| Context     | Shared: Injected into your current chat; uses the same memory. | Isolated: Runs in a separate "sandbox" to save tokens/noise. |
| Execution   | Passive: It gives the AI "knowledge" on how to do a task.      | Active: It takes over, runs commands, and returns a result.  |
| Trigger     | Automatic: Loaded when the AI detects it needs that expertise. | Delegated: The main AI "spawns" it to handle a sub-task.     |
| Best For    | Coding standards, API docs, or repetitive "how-to" steps.      | Complex research, long-running tests, or security audits.    |
| Analogy     | A YouTube Tutorial on how to fix a leaky pipe.                 | A Plumber you hire to actually fix the leak for you.         |