---
title: "Source: Agent Auto-Correction & Workflow Files (Claude Code Agent Tutorial)"
---

Condensed extraction from the tutorial *"How to Build an AI Agent with Claude Code"*, the same source already logged in [[ai-agent-system-instructions|AI Agent System Instructions]]. That note covers how to write the instruction file; this one covers two follow-on topics: how an agent corrects course under uncertainty, and how to structure a reusable Workflow File (Agent SOP).

Distilled from `agent-autocorrect-workflow-guidelines.md`, downloaded 2026-09-25.

## Auto-correction and discernment

The tutorial treats course-correction based on discernment (reasoning through uncertainty and ambiguity) as the main dividing line between a chatbot and an agent.

### 1. Stop and ask instead of guessing

- A chatbot behaves like fancy autocomplete: given an ambiguous request it guesses intent and pattern-matches to the most probable answer.
- An agent shows discernment under uncertainty: when context is missing or direction is ambiguous it stops and asks rather than making unverified assumptions.
- Standing rule to put in the instruction file (`CLAUDE.md`): *"Always ask at least three clarifying questions before starting any complex task."*
- Why it works: unverified assumptions cause most mediocre AI output, so clarifying up front removes them before execution starts.

### 2. Plan before executing

- An autonomous agent commits to a direction, creates files and structures content. If its first assumptions are wrong, the cleanup is a half-finished, flawed project.
- Planning mode makes the agent pause, show how it read the goal, list the steps and files it will create, and surface open questions before acting.
- Standing rule: *"Always present a written plan and wait for approval before beginning any multi-step task."*
- Why it works: a two-minute plan review routinely saves ten minutes of cleanup.

### 3. Review and adjust during execution

- A real agent works in phases: gather context, form a plan, execute step by step, review its own work, adjust if something is not working.
- If the direction turns out wrong mid-run, it adapts to what it found instead of pushing on with a bad assumption.
- Because it works in a persistent workspace it keeps context of what it generated, so targeted feedback updates the existing file rather than starting over.

## The four pillars of a Workflow File (Agent SOP)

A Workflow File is a plain Markdown document acting as the standard operating procedure for one task or role. It replaces a one-off prompt with a repeatable system built from four parts.

| Pillar | What it defines | Why it matters |
|---|---|---|
| **Goals** | The outcome: exact scenario, target audience, desired depth (e.g. "research how non-technical marketing teams use AI agents for content creation") | Vague goals produce generic output |
| **Constraints** | Non-negotiable boundaries: word limits, file-naming rules (e.g. lowercase with hyphens), tool restrictions, human-approval triggers before touching key files | Prevents scope creep and lazy or dangerous behaviour |
| **Format** | Layout, structural template, tone, file requirements (e.g. clean Markdown or PDF saved to an output directory) | Without it the agent defaults to verbose, unpredictable prose |
| **Failure** | What to do when something breaks, data is missing, or the request is ambiguous: stop, ask, or surface the error | Without it the agent guesses or hallucinates |

## Pitfalls that break course correction

1. **Skipping the plan review.** An agent that executes without a reviewed plan drifts further off track, and cleanup costs more than adjusting the plan.
2. **Omitting the clarification rule.** If the instruction file never says to ask first, the agent guesses, and the guesses become the mediocre output.

## Related notes

- [[ai-agent-system-instructions|AI Agent System Instructions]]: the six-part anatomy, where these two standing rules appear as part 3.
- [[../templates/system-instructions|System Instructions templates]]: includes a Workflow File skeleton built from the four pillars.
