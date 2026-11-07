---
title: Advanced Prompting Techniques
reviewed: 2026-11-07
---

Techniques for work where a wrong answer is costly: plans, designs, analyses, long agent runs. Synthesised from [[../sources/prompt-optimization-guide|Prompt Optimization Guide]], [[../sources/vendor-guidance-2026|Vendor Guidance 2026]], [[../sources/google-prompt-engineering-whitepaper|Google whitepaper]] and [[../sources/mastering-claude-ai|Mastering Claude AI]] Ch.10. Basics are in [[foundational|Foundational Techniques]].

**Ask for artefacts, not reasoning.** Current models think internally (always on for Fable 5.1 and Opus 5.5). Every technique below asks for something you can read and check: a weakness list, a revised draft, a rubric result. Do not ask the model to write out its reasoning in the answer; that duplicates its thinking, and Fable 5.1, Opus 5.5 and Sonnet 5.5 may decline it as reasoning extraction (Anthropic, checked 2026-11-07). See [[retired|Retired Techniques]].

## Review techniques

### 1. Draft, critique, revise
One prompt: give a draft, list its three biggest weaknesses, then a revised version. A self-review without back-and-forth. Replaces the older "recursive chain of thought" ladders, which prescribed the thinking instead of the output. (Prompt Optimization Guide)

### 2. Adversarial review
The model attacks a draft, plan or design as a skeptical reviewer, looking for failure scenarios, risks and bias. Unlike a quality check, it assumes something is wrong and hunts for it. Ask for concrete failures ("input X produces wrong result Y"), not general concerns.

### 3. Multi-perspective
Argue the problem from named viewpoints (sponsor, skeptic, end user, operator), then synthesise one recommendation. Counters the pull toward the most agreeable answer. Variants: "how would a [role] approach this?", or analysis across stakeholder impact, resources, risk, timeline and success metrics. (Prompt Optimization Guide, Mastering Claude AI App. A)

### 4. Rubrics
Define good as a handful of yes-or-no checks and have the model check its output against them before answering, reporting any that fail. The same idea scales to agents as a definition of done. (Prompt Optimization Guide)

### 5. Step-back
First ask a general question ("what makes a migration plan safe?"), then feed the answer into the specific task. Pulls in background knowledge before the model commits to specifics. (Google p.25-28)

## Prompt improvement

### 6. Meta-prompting
- **Before the task:** "What would you need from me to do this well?" Finds missing context for the cost of one turn.
- **On the prompt:** ask the model to rewrite your prompt, critique its rewrite, and give a final version under a length cap (rewrites bloat).
- **Conflict check:** ask it to list contradictory or redundant instructions, then make surgical edits. Typical conflicts: brevity vs. completeness, autonomy vs. asking first. (OpenAI GPT-5.1 guide)

### 7. Evaluate, do not eyeball
For prompts you reuse: a small test set of real inputs, explicit criteria scored per run, a log of each version and result. Re-run it when the model changes. A model or LLM judge can score runs; you still decide what counts as good. (Google p.62-63, Mastering Claude AI Ch.10)

### 8. Compare runs and tiers
- Run the same prompt two or three times; where answers disagree, the task is under-specified or genuinely uncertain.
- Run it on two model tiers; if results match, the cheaper tier is enough for that kind of task. (Prompt Optimization Guide)

## Creative techniques

### 9. Constraint engineering
Extreme constraints ("zero budget, no new technology, live by tomorrow") push past the generic answer. Produces novel, not good, ideas: run a feasibility filter afterwards. **Cascading variant:** explain the idea at shrinking budgets (full, half, half again, one metaphor, one question); what survives every cut is the core. (Mastering Claude AI Ch.10)

### 10. Brainstorm with a quota for the unusual
"Ten approaches, at least three unconventional." Forces range before convergence. (Mastering Claude AI App. A)

## Long-running and agentic work

- **State the completion condition up front** and keep the parts in a checklist the model updates (a to-do tool or a file).
- **Treat a text-only end of turn as a report, not proof of completion.** If items remain open and no blocker is stated, name them and ask it to continue; stop after two or three automatic continuations. (Anthropic, Opus 5.5 guide)
- **Name the early stops you do not want** (summary that announces the next step instead of taking it; offering to wait) and the ones you do (blocked on the user). Keep confirmation for risky or irreversible actions.
- **Tell it about context limits** when the harness compacts or saves state, so it does not wrap up early.
- **Tests or checks first** for multi-session work, tracked in a structured file.

## Which technique, when

| Situation | Use |
|---|---|
| Quick, clear task | Foundational only |
| Ambiguous or high-stakes ask | Ask first (meta-prompting before the task) |
| Plan, design or recommendation | Draft, critique, revise, plus adversarial review |
| Contested decision | Multi-perspective |
| Output must meet a standard | Rubric |
| Reusable prompt | Evals, conflict check, compare tiers |
| Creative block | Constraint engineering, brainstorm quota |
| Long agent run | Completion condition, checklist, continuation rule |

## When a technique is failing

Signs: answers get longer but not better, reasoning turns circular, output ignores practical limits, the process has become more complex than the problem. Recover: go back to a plain, well-specified prompt; verify key claims independently; get domain input; test small before rollout. Some problems are not prompt-shaped. (Mastering Claude AI Ch.10)
