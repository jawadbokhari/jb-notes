---
title: "Template: Task Workflow"
---

A lightweight standard operating procedure for one repeatable task that an existing agent runs, so the task does not need re-explaining each time. Built from the four pillars in [[../sources/agent-autocorrect-and-workflow-files|Agent Auto-Correction & Workflow Files]], updated with [[../guidelines/system-prompt-guidelines|the guidelines]]. It inherits the user and area instructions; do not repeat them.

Use this instead of an [[agent-contract|Agent Contract]] when the task has no tools, scope or hand-back of its own. In Claude Code it usually becomes a skill or slash command.

```markdown
# Workflow: [Task name]

## Goal
- **Outcome:** [the exact result, e.g. "a one-page competitor brief"].
- **For:** [audience and what they will do with it].
- **Depth:** [e.g. "5 competitors, 3 dimensions each"].

## Inputs
- [What the user provides]. If missing, ask for it before starting.

## Constraints
- [Length limit].
- [Naming or location rule], because [reason].
- [Tools allowed, or excluded].
- Ask before [touching key files, sending anything].

## Steps
<!-- Only where order matters. -->
1. [Step].
2. [Step].
3. Check against "Done when" below.

## Format
- **Deliverable:** [e.g. "Markdown file in ./output/"].
- **Structure:** [headings, table, named template].
- **Tone:** [e.g. "direct, concise"].

## If something goes wrong
- Missing data or source: stop and name it; do not assume.
- Ambiguous request where a wrong guess is costly: ask. Otherwise assume and state the assumption.
- Tool fails or the approach proves wrong mid-run: report it and propose an adjusted plan.

## Done when
- [ ] [Checkable criterion].
- [ ] [Checkable criterion].
- [ ] Report lists skipped steps first, then result, then anything done unasked.
```

Changes from the original Workflow File: "ask at least three clarifying questions" became trigger-based asking; a "Done when" section was added; the plan-first rule moved up to the user level, where it applies everywhere.
