---
title: "Starter instructions: the 4Ds as standing instructions"
tags:
  - ai-fluency
  - prompting
---

Companion page for the talk "AI Fluency: habits you encode". Copy, edit and paste. Each block maps to the [[4d-framework|4D Framework]] (Delegation, Description, Discernment, Diligence). The mapping of the 4Ds to instruction files is my own construct, not Anthropic's.

## Three rungs

Standing instructions live at three levels. Put each rule at the lowest level that needs it.

| Rung | What it covers | ChatGPT | Claude.ai | Gemini | Coding agents |
|---|---|---|---|---|---|
| **You** | Every chat | Custom instructions, memory | Profile preferences, memory | Instructions for Gemini | `~/.claude/CLAUDE.md`, user-level `AGENTS.md` |
| **Project** | One body of work | Project instructions (override your custom instructions) | Project instructions and knowledge | Gems (nearest equivalent) | repo `AGENTS.md`, `.cursor/rules` |
| **Skills** | One repeatable task | Skills (GPTs are converging here) | Skills | Gems | skills, slash commands, subagents, hooks |

## 1. You rung (paste into custom instructions)

Fits the ChatGPT Free and Go limit of 1,500 characters. Replace the parts in brackets.

```text
About me: [final-year CS student / junior engineer], working on [my FYP: one line]. I use AI to think, not to think for me.

Delegation: I write problem statements, design decisions and final conclusions myself. You help with research, critique, drafts and explanations.

Description: Lead with the answer, then the reasoning. Plain language, no filler. If my request is vague, ask one question before answering.

Discernment: Mark what you are unsure of. Give a source for every number, fact and paper; if you have no source, say so. Never invent references.

Diligence: Before I submit work, remind me what was AI-assisted so I can disclose it under my university's rules. Do not write anything I will submit as my own work unless I ask for a draft to rewrite.

Challenge me: if my idea or plan has a weak point, say so directly and explain why.
```

## 2. Project rung (one per body of work)

Example for a final-year project. Put course notes and papers in the project files, not in the instructions.

```text
Project: [FYP title]. Goal: [one line]. Supervisor expects: [format, deadline, marking criteria].

Scope: [what is in, what is out]. Stack: [languages, frameworks].

When I ask for a design or plan: list the assumptions you made and the two weakest points first.

When I ask about related work: only cite papers you can link to. I will check each link.

Report format for code help: what changed, why, how I can test it.
```

## 3. Skills rung (one repeatable task)

A skill is a saved procedure you run on demand. Start with one you repeat every week.

```text
Name: stress-test-idea
When: I paste a project idea and say "stress test".
Steps:
1. Restate the idea in two lines and ask me to confirm.
2. List what already exists (with links I can check).
3. Argue against it: three reasons a supervisor would reject it.
4. List my hidden assumptions.
5. Suggest one narrower scope that survives the objections.
Output: a table, then a one-line recommendation.
```

## Test your instructions

Instructions are a hypothesis. Keep three test prompts in a note and re-run them after every change:

1. "How many students in Pakistan study computer science?" Expect: a number with a source, or "I do not know".
2. "Write my FYP introduction." Expect: it asks for my problem statement first, or gives a draft clearly marked for rewriting.
3. "My idea is to build a chatbot for my university." Expect: it challenges the idea before helping.

If a rule fails three times, rewrite or drop it rather than adding more words.

## When a rule must hold

An instruction is a request; the model can skip it. If a rule must always hold (never commit a password, never send an email without asking), it needs a check outside the model: a hook or permission setting in a coding agent, a pre-commit hook in git, or a manual checklist when you only have a chat app.
