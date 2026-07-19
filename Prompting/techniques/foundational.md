---
title: Foundational Prompting Techniques
---

Source: [[../sources/mastering-claude-ai|Mastering Claude AI]], Ch.4.

## Anatomy of a good prompt
Four ingredients — missing any one degrades the response:

| Ingredient | Question it answers | Example |
|---|---|---|
| Context | What's the situation? | "I'm emailing a client after our first meeting" |
| Specificity | What exactly do I want? | "5-slide outline, 10-min talk, HS students" |
| Format | How should it look? | "as a table with 3 columns" |
| Constraints | What are the boundaries? | length / tone / audience / scope |

Rule of thumb: vague in → vague out. Specificity beats vagueness, but don't stack so many constraints they conflict (see pitfalls below).

## Few-shot learning
Show, don't just describe:
- **Zero-shot** — no examples, just the instruction
- **One-shot** — one example to imitate
- **Few-shot** — multiple examples; Claude infers style/tone/structure as a pattern, not a template to copy verbatim

Use when: tone/format is hard to describe in words but easy to demonstrate (brand voice, a specific writing style, code style).

## Role-playing
"You're a [role] with [trait]. [Task], for [audience]." Bundles expertise level + tone + approach into one instruction. Cheap and effective — usually the first thing worth trying when a plain instruction reads generically.

## Chain of thought (basic)
Ask for step-by-step reasoning before the conclusion. Best for problems with verifiable intermediate steps (multi-factor decisions, debugging, analysis). Caveat: Claude emulates plausible-sounding reasoning patterns from training data — it is not doing formal logic. Treat the reasoning as a structuring device, verify conclusions independently, especially outside domains with strong training-data conventions.

## Iteration
Nobody nails it in one shot. Cycle: **attempt → analyze what's working/missing → refine → repeat.** Starting simple and iterating beats trying to perfect the first prompt (see "Perfectionist Paralysis" below).

## Meta-prompting (basic)
Ask Claude what it needs from you before doing the task: *"I want help with [goal]. What information/context would you need from me to do this well?"* Cheap way to discover missing context before wasting a round-trip.

## Five pitfalls to check for
1. **Kitchen Sink** — one prompt asking for write+edit+format+optimize → split into steps
2. **Mind Reader Fallacy** — assuming implied intent is obvious → state it
3. **One-Size-Fits-All** — same template regardless of task type → code prompts ≠ poetry prompts
4. **Perfectionist Paralysis** — polishing prompt #1 forever → ship a draft, iterate
5. **Over-Constraining** — stacking specific criteria until they conflict → relevant specificity, not maximal

## Pre-send checklist
- [ ] Enough context?
- [ ] Specific and clear?
- [ ] Format specified?
- [ ] Constraints reasonable and compatible with each other?
- [ ] Would an example clarify this faster than more description?
- [ ] Asking for one thing at a time?
- [ ] Backup approach ready if this doesn't land?

## Skill progression (self-check)
Novice → "Help me write." Intermediate → topic + length. Advanced → topic + audience + tone + structure + exclusions, in one prompt. Master → same result reached conversationally, adapting technique to what the response reveals.

See also: [[advanced|Advanced Prompting Techniques]]
