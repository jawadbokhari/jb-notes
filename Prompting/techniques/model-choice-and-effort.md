---
title: Model Choice and Effort
reviewed: 2026-11-11
---

Which Claude model and effort level to give a task, and when to escalate. Sources: [[../sources/anthropic-which-claude-model|Which Claude Model Should You Build With?]] (Anthropic blog, accessed 2026-11-11), Anthropic "Choosing a model", "Effort" and "Prompting Claude Opus 5.5" pages (see [[../sources/vendor-guidance-2026|Vendor Guidance 2026]]), and [[../sources/prompt-optimization-guide|Prompt Optimization Guide]]. Model line-ups change; re-check the sources when a new model ships.

**Rule one:** fix the prompt before changing the model. If your corrections are mostly clarifying what you meant, a bigger model will not help.

## Models (Claude, November 2026)

| Model | Use for | API price in / out per M tokens |
|---|---|---|
| Opus 5.5 | Default for most work: everyday engineering and debugging, knowledge work, vision-heavy and computer-use loops | $4 / $20 |
| Sonnet 5.5 | Well-scoped work: bug fixes, features against a spec, everyday documents and slides, chat, repeated agent tasks (review, drafting, investigation) | $2 / $10 |
| Haiku 5.5 | Classification, routing, extraction at volume; subagents that search files, read logs or summarise | $0.10 / $0.50 (prompts up to 100K) |
| Fable 5.2 | Major refactors and migrations, architecture planning, leading many subagents, deep research, quantitative analysis, long unattended runs | $8 / $40 |

A clear spec does not make a task Sonnet work: a specced migration or performance optimisation can still need Opus, or Fable if it is major.

## Planning which model gets a task

Ask in this order:

1. **Is a wrong answer cheap to spot?** (search, log reading, file finding, test runs, classification) Haiku, or Sonnet if the reading needs more judgment.
2. **Is the task well scoped and repeated or routine?** (bug fix, spec'd feature, drafting, review pass, a deck) Sonnet at `medium`.
3. **Does it need judgment, edits across a codebase, or long agentic loops?** Opus at `medium`.
4. **Is it the hardest work you have, or will it run unattended for hours?** Fable at `medium`, then `high`.
5. **Unsure?** Opus at `medium`.

In a multi-agent setup: keep code edits and judgment calls on the main model and give smaller models only work where a mistake is cheap to spot, because a misread search result sends the main model down the wrong path. For work larger than one context window, an Opus lead with Sonnet workers cost about a third less than Opus alone at about the same score in Anthropic's test. Skip the lead-and-workers pattern for a chain of dependent steps or work that fits one context.

## Effort

- Effort is the main control for how much the model thinks. Thinking is always on for Fable 5.2 and Opus 5.5; effort, not prompt wording, sets how much.
- Defaults: `medium` on Opus 5.5 and Haiku 5.5. Sonnet 5.5 and Fable 5.2 default to `high` on the API and `medium` in Claude Code (`/effort status` shows yours).
- Level names do not mean the same across models: do not carry a setting over from an older model.
- Fable 5.2 at `high` and above thinks before almost every reply, and "answer directly" in the prompt does not stop it at `medium` and above. Lower the effort instead (Anthropic prompting best practices, accessed 2026-11-11).
- Cost curve on Opus 5.5 (SWE-bench Pro, relative to `high`): `medium` about 2.5 points lower at 70% of the cost, `low` about 8 points lower at a third, `xhigh` about 1.4 points higher at 2.5 times the cost.
- Past `high`, one more level can cost as much as the next model up. Test the bigger model at a lower effort instead.
- Effort cannot add knowledge or skill the model lacks; only a bigger model does.
- For latency-sensitive replies a person waits on, start Sonnet at `low` or `medium`.

## When a model falls short

Take these steps in order:

1. Give it a way to verify its own work (a test, a build, a script that calls the endpoint). This is often cheaper and faster than more effort.
2. Raise effort one level.
3. Move up one model, starting at a lower effort than you used on the smaller one.

Signs it is time for Fable:

- Opus at `high` has missed twice on the same problem, with a clear prompt.
- A wrong answer would surface only late (architecture decisions, long unattended agent runs).
- You keep fixing the same kind of flaw across rounds.

If outcomes can be checked automatically, run everything at a low effort and re-run only the failures at a high one: about 97% pass at $0.17 per task against 95.3% at $0.29 with every task at `high`, in Anthropic's test.

## Cost habits

- Price per token is not cost per task: Fable 5.2 at `high` matched Opus 5.5 at `max` on FrontierCode 2.0 at about half the cost per task.
- The hardest tasks carry most of the spend; price them, not only the typical ones.
- Context is billed every turn. Keep the expensive model's context lean and let cheaper subagents do the verbose reading.
- Switch models at a natural break: the cache belongs to the model that wrote it, so `/compact` or start fresh with a short written plan. Moving down a tier also drops the earlier model's thinking.

## Claude Code settings

- Pin a subagent's model with `model: haiku` or `model: sonnet` in its definition; `CLAUDE_CODE_SUBAGENT_MODEL` sets the default for the rest.
- The built-in Explore subagent runs on the session model. Define your own `Explore` with `model: haiku` to keep exploration cheap.
- `opusplan` (Opus plans, Sonnet edits) puts code edits on the smaller model, the reverse of the advice above. Measure before making it a default.

## Check whether a cheaper tier is enough

Run the same task on two tiers (`/model`, then compare `/usage`). If outcomes match, use the lower tier for that kind of task. For anything run at volume: sample real tasks with an outcome check, run each candidate at two or three effort levels in separate sessions, plot score against spend, and keep a multi-model setup only if it beats every single-model point.
