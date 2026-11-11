---
title: "Source: Prompt Optimization Guide (working guide, November 2026)"
source_type: practitioner
currency: current
reviewed: 2026-11-07
---

A short working guide on improving prompts and choosing a Claude model, captured in the vault inbox on 2026-11-07. Author and origin not recorded; it states its model advice is "per Anthropic's docs". Model claims below were checked against Anthropic's documentation on 2026-11-07 (see "Checked against primary sources"). Distilled into [[../techniques/foundational|Foundational Techniques]], [[../techniques/advanced|Advanced Techniques]] and [[../techniques/model-choice-and-effort|Model Choice and Effort]].

## Core idea

Most rework comes from the prompt, not the model. Missing context, unstated intent or unclear success criteria force the model to guess. Fix the prompt first; escalate the model second.

## Model choice

- Start with Opus 5.5 for most workloads.
- Sonnet 5.5 for everyday work where speed matters more than depth.
- Haiku 5.5 for high-volume or fan-out work.
- Fable 5.1 for demanding reasoning and long-running agentic work, or when Opus at higher effort still falls short. The guide says it is opt-in, not the default on any plan.
- Effort: start with the default, then adjust on your own results. Up for capability-sensitive work, down for routine or latency-sensitive work.

**When to escalate to Fable:**
- Opus at high effort has missed twice on the same problem, with a clear prompt.
- A wrong answer would only surface late (architecture decisions, long unattended agent runs).
- You keep fixing the same kind of flaw across rounds.

If your fixes are mostly clarifying what you meant, the prompt is the problem and a bigger model will not help.

## Techniques

1. **Ask-first (Socratic) prompting.** The model lists what is ambiguous or missing and asks a few questions before starting. For ambiguous or high-stakes tasks. Costs a turn, saves a rework round.
2. **State intent, not just the task.** What the output is for, who uses it, what a bad answer looks like.
3. **Draft, critique, revise.** In one prompt: draft, list three weaknesses, second draft.
4. **Adversarial review.** The model attacks a draft, plan or design as a skeptical reviewer, hunting for failure rather than checking quality.
5. **Multi-perspective prompting.** Argue the problem from several viewpoints (optimist, skeptic, end user), then synthesize one recommendation. Counters the pull toward the most agreeable answer.
6. **Meta-prompting.** The model rewrites your prompt, optionally critiquing its own rewrite first. Cap the length; rewrites bloat.
7. **Rubrics.** A handful of yes-or-no checks the model applies to its output before answering.
8. **Examples as demonstrations.** One or two examples of expected output, including an accept or refuse case where edge cases matter.
9. **Compare across tiers.** Run the same prompt on two model tiers; if answers match, the lower tier is enough for that kind of problem.

## Draft standing instruction (as given)

> If the request is clear, just do it. If something is ambiguous, make a reasonable assumption, state it in one line, and carry on. Ask a question only when a wrong guess would be costly or hard to undo, and never more than two. For plans and designs, argue against your own recommendation once before finalizing. For complex or high-stakes work, give a draft, list its three biggest weaknesses, then a revised version. Keep it terse. Skip the preamble.

## Trade-offs

- Ask-first adds a turn; skip it for simple, low-risk tasks.
- Adversarial and multi-perspective prompts add length; use them where a wrong answer is costly.
- Over-prompting backfires on newer models. Prefer targeted instructions over blanket rules.

## Prompt libraries and skills listed

Seven GitHub prompt and skill collections, unvetted. Kept in [[../prompt-and-skill-libraries|Prompt and Skill Libraries]].

## Checked against primary sources (2026-11-07)

| Claim in the guide | Anthropic docs say | Verdict |
|---|---|---|
| Start with Opus 5.5 for most workloads | "Most workloads start with Claude Opus 5.5" (`platform.claude.com/docs/en/about-claude/models/choosing-a-model`) | Confirmed |
| Fable 5.1 when Opus at higher effort falls short | Move to Fable 5.1 "if your evals at `xhigh` or `max` effort still fall short on demanding reasoning or long-horizon agentic work" (same page) | Confirmed |
| Fable is opt-in, not the default on any plan | Not stated on the pages checked | Unverified |
| Start effort at the default | Default is `medium` on Opus 5.5 and Haiku 5.5, `high` on Fable 5.1, Opus 5 and Sonnet 5.5; effort level names do not mean the same thinking across models | Confirmed, with per-model defaults |
| "Opus at high effort missed twice" as escalation trigger | Docs escalate on evals at `xhigh` or `max`, not a miss count | Author's heuristic, reasonable for chat use |
| Over-prompting backfires on newer models | Aggressive wording ("CRITICAL: You MUST") overtriggers; soften it (`.../claude-prompting-best-practices`) | Confirmed |
| "Never more than two" questions | Not in vendor docs; a quota, which [[../guidelines/system-prompt-guidelines\|the guidelines]] replace with triggers | Keep the triggers, drop the count |
