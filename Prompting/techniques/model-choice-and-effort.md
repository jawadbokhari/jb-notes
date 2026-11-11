---
title: Model Choice and Effort
reviewed: 2026-11-07
---

Which Claude model and effort level to use, and when to escalate. Sources: Anthropic "Choosing a model", "Effort" and "Prompting Claude Opus 5.5" pages, accessed 2026-11-07 (see [[../sources/vendor-guidance-2026|Vendor Guidance 2026]]), and [[../sources/prompt-optimization-guide|Prompt Optimization Guide]]. Model line-ups change; re-check the sources when a new model ships.

**Rule one:** fix the prompt before changing the model. If your corrections are mostly clarifying what you meant, a bigger model will not help.

## Models (Claude, November 2026)

| Model | Use for |
|---|---|
| Opus 5.5 | Default for most work: agentic coding, knowledge work, vision-heavy and computer-use tasks |
| Sonnet 5.5 | Everyday work where speed matters more than depth |
| Haiku 5.5 | High-volume, latency-sensitive or fan-out work, sub-agent tasks |
| Fable 5.1 | Highest capability: hours-long agent sessions, deep research, analysis carried to a finished document; when Opus at `xhigh` or `max` still falls short |

## Effort

- Effort is the main control for how much the model thinks. Thinking is always on for Fable 5.1 and Opus 5.5; effort, not prompt wording, is how you get more or less of it.
- Start at the model's default and adjust on your own results: `medium` on Opus 5.5 and Haiku 5.5, `high` on Fable 5.1, Opus 5 and Sonnet 5.5.
- Level names do not mean the same across models: Opus 5.5 at `medium` matches or beats Opus 5 at `high` in Anthropic's testing. Do not carry an effort setting over from an older model.
- Go up for capability-sensitive work; reserve `xhigh` and `max` for work where you have seen a quality gain. Go down for routine or latency-sensitive work.
- Tuning effort is often a better lever than switching models.

## When to escalate to Fable

- Opus at high effort has missed twice on the same problem, with a clear prompt.
- A wrong answer would surface only late (architecture decisions, long unattended agent runs).
- You keep fixing the same kind of flaw across rounds.

## Check whether a cheaper tier is enough

Run the same prompt on two tiers. If the answers match, use the lower tier for that kind of task.
