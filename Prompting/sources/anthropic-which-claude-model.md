---
title: "Source: Which Claude Model Should You Build With? (Anthropic, November 2026)"
source_type: vendor-blog
currency: current
reviewed: 2026-11-11
url: https://claude.dev/blog/which-claude-model-should-you-build-with/
---

Anthropic engineering blog post on picking a Claude model and effort level, pricing, mixing models and migration checks. Accessed 2026-11-11. Covers Haiku 5.5, Sonnet 5.5, Opus 5.5 and Fable 5.2 (Mythos 5.2 is verification-programme only). Distilled into [[../techniques/model-choice-and-effort|Model Choice and Effort]].

## Headline advice

- Start most work on Opus 5.5 at `medium`. It is the Claude Code default and costs half of Fable 5.2 per token.
- Down to Sonnet 5.5 for well-scoped everyday work (bug fix, feature against a spec). A clear spec alone is not enough: a migration or performance optimisation can be specced and still need Opus, or Fable for a major one.
- Down to Haiku 5.5 for classification, routing, extraction, and subagent side tasks.
- Up to Fable 5.2 for the hardest coding, finance and science work, when Opus at `high` still falls short, or for long unattended runs.
- Try effort before switching model. Past `high`, one more effort level can cost as much as the next model up, so test the bigger model at a lower effort instead. Effort cannot add knowledge or skill the model lacks.

## Task table (starting model and effort)

| Task | Model | Effort |
|---|---|---|
| Everyday engineering, debugging, multi-PR features | Opus 5.5 | `medium`, then `high` |
| Classification, routing, tagging, high-volume extraction | Haiku 5.5 | `medium` |
| Subagents that search files, read logs, summarise | Haiku 5.5 or Sonnet 5.5 | default |
| Chat and interactive sessions | Sonnet 5.5 (Haiku for simple chat at volume) | `low` or `medium` |
| Well-scoped coding (bug fixes, iteration, spec-driven) | Sonnet 5.5 | `medium`, then `high` |
| Everyday documents, slides, spreadsheets | Sonnet 5.5 (Opus for complex financial models or large source piles) | `high` (`medium` in Claude Code) |
| Repeated agent tasks (investigation, review, drafting) | Sonnet 5.5 | `medium` |
| Computer use and vision-heavy loops | Opus 5.5 | `medium` |
| Major refactors and migrations, architecture planning, leading many subagents | Fable 5.2 | `medium`, then `high` |
| Deep research, scientific or quantitative analysis | Fable 5.2 | `medium`, then `high` |
| Unsure | Opus 5.5 | `medium` |

## Prices and specs (Claude API list, per million tokens)

| | Haiku 5.5 | Sonnet 5.5 | Opus 5.5 | Fable 5.2 |
|---|---|---|---|---|
| Input / output | $0.10 / $0.50 up to 100K prompt; $0.50 / $2.50 over | $2 / $10 | $4 / $20 | $8 / $40 |
| Cache read | $0.01 / $0.05 | $0.10 | $0.20 | $0.20 |
| Latency | fastest | fast | moderate | moderate |
| Default effort, API (Claude Code) | `medium` | `high` (`medium`) | `medium` | `high` (`medium`) |
| Fast mode | no | no | yes | yes |

All four: 1M context, 128K max output.

## Trade-offs, with the article's numbers

- **Price per token is not cost per task.** Terminal-Bench 3.0: Fable 5.1 at `max` 58.0%, Opus 5.5 at `high` 58.9% on half the tokens. FrontierCode 2.0: Fable 5.2 at `high` 45.3% vs Opus 5.5 at `max` 45.5%, Fable at about half the cost per task.
- **Hard tasks carry the spend.** On one 20-problem benchmark, two problems were 43% of spend. Price the hardest tasks, not only the typical ones.
- **Effort curve, Opus 5.5 on SWE-bench Pro** (relative to `high`): `medium` about 2.5 points lower at about 70% of cost; `low` about 8 points lower at about a third; `xhigh` about 1.4 points higher at 2.5 times the cost.
- **Low first, re-run failures high.** Opus 5.5 at `low` with failures re-run at `high`: about 97% pass at about $0.17 per task, vs 95.3% at $0.29 with everything at `high`. Needs an automatic outcome check.
- **When a model falls short, in order:** (1) give it a way to verify its own work (test, build, script); (2) raise effort one level; (3) move up one model, starting at a lower effort than you used below.
- **Context costs every turn.** Cache read on Opus 5.5 is about $0.03 per turn at 150K context, $0.004 at 20K. Keep the expensive model's context lean; let cheaper subagents do the verbose reading.
- On cache-heavy runs Fable and Opus cost the same for cache reads; the gap is uncached input and output.
- Haiku's over-100K tier is five times its short rate. For long prompts, compare Haiku and Sonnet on cost per finished task.

## Mixing models

- **Switch at a natural break.** The prompt cache belongs to the model that wrote it, so the first turn on a new model rewrites the whole conversation to cache. `/compact` first, or start fresh with a short written plan.
- **Thinking blocks do not travel down.** A model never reads the thinking of a model above it; moving off Fable 5.2 drops its reasoning. Opus reads Sonnet and Haiku; Fable reads Opus, Sonnet and Haiku.
- **Subagents on smaller models** for work where a mistake is cheap to spot: finding files, running tests, reading logs. Keep code edits and judgment calls on the main model, because a misread search result sends the main model down the wrong path.
- **Claude Code specifics:** set `model: haiku` or `model: sonnet` in a subagent definition; `CLAUDE_CODE_SUBAGENT_MODEL` sets the default. The built-in Explore subagent now runs on the session model, not Haiku; define your own `Explore` with `model: haiku` to keep exploration cheap. `opusplan` (Opus plans, Sonnet edits) is the reverse of this advice; measure before adopting.
- **Advisor tool (beta):** cheap executor consults a stronger advisor. Platform data is weak: none of four pairings clearly beat the executor alone; Opus 5.5 `high` plus Fable 5.1 advisor gained 1.7 points for 2.1 times the cost. Measure the consult rate first.
- **Lead plus cheap workers** for work larger than one context: Opus 5.5 lead with up to 25 Sonnet 5.5 workers over about 22M tokens of code cost about a third less than Opus alone, at about the same score. Skip for dependent step chains or work that fits one context.

## Migration checks (API)

- Fable 5.2 returns 400 if anything before its thinking block changed (system prompt, tools, earlier messages) unless you opt in to dropping it. Keep history append-only. Claude Code, Agent SDK and Managed Agents handle this.
- Opus 5.5 and Fable 5.2 always think; turning thinking off errors. Read content blocks by `type`.
- `tool_choice` `any` or `tool` returns 400 on Sonnet, Opus and Fable 5.x: send `auto`, mark the tool `strict: true`, say when to use it in the prompt.
- Haiku 4.5 to 5.5: effort instead of `budget_tokens`; drop non-default `temperature`, `top_p`, `top_k`; end `messages` with a user turn.
- Safety classifiers on Opus, Sonnet and Fable flag cyber and bio content most; in Claude Code a flagged request can re-run on an older model (cyber to Opus 4.8, bio to Opus 5).
- Multi-model systems: build every request for the strictest model so a step can move tiers without code changes. When routing is a simple rule (one model per step type), let code choose, not a model.

## Measuring on your own work

1. Sample real tasks, each with an outcome check (passing test, closed ticket, correct row count).
2. Run each candidate at two or three effort levels, separate sessions so caches are not shared; record cost per completed task from `usage`.
3. Plot score against spend; keep a multi-model setup only if it beats every single-model point.
4. Shadow the winner on real traffic before cutting over.

Quick check in Claude Code: run one backlog task on two models with `/model`, compare `/usage`.
