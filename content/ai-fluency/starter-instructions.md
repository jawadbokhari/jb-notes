---
title: "Starter instructions: brief your AI colleague"
tags:
  - ai-fluency
  - prompting
---

Companion page for the talk "AI Fluency: work with AI like a new colleague". Copy, edit and paste. A new colleague needs two things: a clear request for each job, and a proper brief on day one. This page gives you both. The ladder in the talk (ask, assign, onboard, think together, build a team) is my own construct. The 4D framework it maps to at the end is Anthropic's, from their [[4d-framework|AI Fluency course]].

## Assign: the four parts of a request

When you hand AI a job, tell it four things. Role ("act as...") is optional: it adds tone, not knowledge.

| Part | What you say |
|---|---|
| **Task** | The problem you want solved |
| **Context** | What it needs to know: you, your audience, your material |
| **Output format** | The result you expect: length, structure, form |
| **Success criteria** | How you will judge that it is good |

Example, a cover letter for a data engineer job:

```text
Task: Write a cover letter for this data engineer role.
Context: My CV is attached. The job post is pasted below. I am a final-year CS student with SQL and Python projects.
Output format: 250 words, three paragraphs, plain text.
Success criteria: Names two requirements from the post with proof from my CV for each. Claims nothing that is not in my CV.
```

Without the last three parts you get a cover letter. With them you get yours.

## Onboard: three levels

You brief a new colleague once, not every morning. Standing instructions live at three levels. Put each rule at the lowest level that needs it.

| Level | What it covers | ChatGPT | Claude.ai | Gemini | Coding agents |
|---|---|---|---|---|---|
| **You** | Every chat | Custom instructions, memory | Profile preferences, memory | Instructions for Gemini | `~/.claude/CLAUDE.md`, user-level `AGENTS.md` |
| **Project** | One body of work | Project instructions (override your custom instructions) | Project instructions and knowledge | Gems (nearest equivalent) | repo `AGENTS.md`, `.cursor/rules` |
| **Skill** | One repeatable task | Skills (GPTs are converging here) | Skills | Gems | skills, slash commands, subagents, hooks |

If your app does not offer one of these, use the nearest thing it has: custom instructions, saved info, or a file you paste at the start of the chat.

## 1. You level (paste into custom instructions)

Fits the ChatGPT Free and Go limit of 1,500 characters. Replace the parts in brackets.

```text
About me: [final-year CS student / junior engineer], working on [my FYP: one line]. I use AI to think, not to think for me.

How we split the work: I write problem statements, design decisions and final conclusions myself. You help with research, critique, drafts and explanations.

How to answer: Lead with the answer, then the reasoning. Plain language, no filler. If my request is vague, ask one question before answering.

Checking: Mark what you are unsure of. Give a source for every number, fact and paper; if you have no source, say so. Never invent references.

Ownership: I submit it, so I own it. Do not write anything I will submit as my own work unless I ask for a draft to rewrite. Tell me what I should verify before I submit.

Challenge me: if my idea or plan has a weak point, say so directly and explain why.
```

## 2. Project level (one per body of work)

Example for a job search. Put your CV, project write-ups and the target job posts in the project files, not in the instructions.

```text
Project: applying for data engineer roles, remote for a US company or in Pakistan. My CV and projects are in the files.

Scope: [what is in, what is out]. Stack: [languages, frameworks].

Every request: I will give you the task, context, output format and success criteria. If one is missing, ask before you start.

When I ask for a design or plan: list the assumptions you made and the two weakest points first.

When I ask about the role or the market: only state what you can link to. I will check each link.

Report format for code help: what changed, why, how I can test it.
```

## 3. Skill level (one repeatable task)

A skill is a saved set of instructions for one kind of task. Start with one you repeat every week. This is the cover letter request from above, saved.

```text
Name: cover-letter
When: I paste a job post and say "cover letter".
Steps:
1. Read the job post and my CV in the project files.
2. Pick the two requirements where my CV has the strongest proof.
3. Write the letter.
Output format: 250 words, three paragraphs, plain text.
Success criteria: names the two requirements with proof from my CV for each; claims nothing that is not in my CV. List any claim you were unsure of after the letter.
```

## Think together

Not sure what to ask yet? Skip the task and ask it to question you first:

```text
I want [goal], but I can't yet say what is missing. Interview me one question at a time, with your recommended answer for each, until we both understand the problem. Then say it back to me and wait for my yes before you start.
```

## Test your instructions

Instructions are a hypothesis. Keep three test prompts in a note and re-run them after every change:

1. "How many students in Pakistan study computer science?" Expect: a number with a source, or "I do not know".
2. "Write my FYP introduction." Expect: it asks for my problem statement first, or gives a draft clearly marked for rewriting.
3. "My idea is to build a chatbot for my university." Expect: it challenges the idea before helping.

If a rule fails three times, rewrite or drop it rather than adding more words.

## Check the work

Looks right is not right. Count what went in and what came out, and compare the total with a number you get another way. You ship it, you own it.

## When a rule must hold

An instruction is a request; the model can skip it. If a rule must always hold (never commit a password, never send an email without asking), it needs a check outside the model: a hook or permission setting in a coding agent (the harness, the code around the model), a pre-commit hook in git, or a manual checklist when you only have a chat app.
