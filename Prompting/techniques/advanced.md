---
title: Advanced Prompting Techniques
---

Source: [[../sources/mastering-claude-ai|Mastering Claude AI]], Ch.10.

> These don't fix fundamental reasoning/knowledge limits — they give more systematic structure to pattern-recognition, so every technique here needs a built-in human validation step.

## 1. Recursive chain of thought
Layered analysis where each level questions and refines the previous one — not just a single linear "show your work."

```
Level 1: Identify the core issue
Level 2: Question Level 1's assumptions — what's missing?
Level 3: Synthesize 1+2 into a refined understanding
Level 4: Find the pattern between initial and refined understanding
Level 5: Apply that pattern to what hasn't been considered yet
```

**Risk**: errors compound across levels. Validate after each level before continuing — if a level is wrong, everything built on it is wrong too. Diminishing returns past ~2–3 levels for most tasks (per Appendix A); go deeper only for genuinely layered problems.

**Variant — self-questioning cascade**: after an initial solution, have Claude ask itself 3 critical questions, answer them, ask 3 deeper questions from those answers, then revise the original solution and explain what changed.

## 2. Meta-prompting loops
Not "ask Claude to help write a prompt" (that's the basic version in [[foundational|foundational techniques]]) — this is a **tracked, multi-round improvement loop** with objective criteria defined *before* starting:

```
Attempt 1 → evaluate: what worked? what to improve? how to adjust next prompt?
Attempt 2 (refined) → evaluate again → ...
```

Rate outputs on defined axes (e.g. clarity 1–10, completeness 1–10, actionability 1–10) instead of vibes — otherwise you can't tell real improvement from noise. AI cannot truly "optimize"; it responds to instructions about improvement — the human is the one evaluating and steering.

## 3. Constraint engineering
Deliberately extreme/"impossible" constraints force exploration outside the default generic answer:

```
Solve [problem] with:
- Zero budget
- No new technology
- Must work for opposing groups
- Implement by tomorrow
- Creates no new problems
```

Produces *novel*, not automatically *good*, ideas. Always run a feasibility filter afterward — many "impossible constraint" solutions sound clever but need real-world modification (legal, resourcing, timing) before they're usable.

**Cascading-constraint variant** — useful for finding the essential core of an idea: explain the same thing at shrinking budgets (full explanation → half the words → half again → one metaphor → a single self-answering question). Whatever survives every cut is the core insight — feed that back into the real explanation, don't ship the stripped version as-is.

## Combining all three
Recursive understanding (what's the real problem?) → meta-prompt evolution (what questions should we actually be asking?) → constraint breakthrough (solve it with only what we already have) → systematic validation (test small, get expert feedback, refine). Each stage has its own quality-check gate — don't chain them without checking.

## Decision framework — which technique, when

| Technique | Use when |
|---|---|
| Simple prompting | Quick answers, straightforward problems, high-stakes facts needing verified info |
| Recursive CoT | Layered analysis needed, assumptions need systematic examination, moderate (non-critical) stakes, time allows multi-step process |
| Meta-prompting | Process improvement is the goal itself, quality is objectively measurable, time for iteration |
| Constraint engineering | Creative block, conventional approaches failing, you have the domain expertise to judge feasibility |

## Recognizing failure and recovering
Signs it's not working: reasoning turns circular/contradictory, improvements plateau or feel artificial, solutions ignore practical requirements, or the process has gotten more complex than the original problem.

Recovery: **simplify back to basic prompting → validate key claims independently → get expert/domain input → test incrementally before full rollout → know when to stop** (some problems aren't prompt-shaped at all).

See also: [[foundational|Foundational Prompting Techniques]]
