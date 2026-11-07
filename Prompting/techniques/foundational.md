---
title: Foundational Prompting Techniques
reviewed: 2026-11-07
---

What every prompt needs, for current reasoning models (Claude 5 family, GPT-5, Gemini 3). Synthesised from [[../sources/vendor-guidance-2026|Vendor Guidance 2026]] (Anthropic prompting best practices, re-checked 2026-11-07), [[../sources/prompt-optimization-guide|Prompt Optimization Guide]], [[../sources/google-prompt-engineering-whitepaper|Google whitepaper]] and [[../sources/mastering-claude-ai|Mastering Claude AI]] Ch.4. Techniques that no longer pay off are in [[retired|Retired Techniques]].

**Core idea:** most rework comes from the prompt, not the model. Missing context, unstated intent or unclear success criteria force the model to guess. Fix the prompt before changing model or effort.

**Key test:** show the prompt to a capable colleague with no context. If they would be confused, the model will be too. (Anthropic)

## 1. Anatomy of a good prompt

| Part | Question it answers | Example |
|---|---|---|
| Context | What is the situation? | "Follow-up email to a client after our first meeting" |
| Intent | What is it for, who reads it, what does a bad answer look like? | "CFO reads it on a phone; a bad answer buries the price" |
| Task | What exactly do I want? | "Three-paragraph email proposing a pilot" |
| Format | How should it look? | "Plain text, no headings, under 150 words" |
| Constraints | What are the limits? | tone, scope, what must not change |
| Done when | How will I judge it? | "Price and start date in the first two lines" |

Intent is the part most often missing, and the part you most often discover later. (Prompt Optimization Guide)

## 2. Give the reason with the instruction

"No ellipses, because a text-to-speech engine reads the output" beats "NEVER use ellipses". The model generalises from the reason to cases you did not list. (Anthropic)

## 3. Say what to do, not what to avoid

"Write flowing prose paragraphs" beats "don't use markdown". Keep prohibitions for safety and hard limits. (Anthropic, Google p.56-57)

## 4. Be literal about scope

Current models follow wording precisely. "Suggest changes" gets suggestions, not edits. If you want more than the task strictly requires (extra polish, tests, alternatives), ask for it. If you want action, say "make the change". (Anthropic)

## 5. Examples: few, varied, tagged

- One to five examples, relevant to the real case, varied so the model does not copy an accidental pattern, with identical formatting.
- Wrap them in `<example>` tags so they are not read as instructions.
- Include an edge case (one to accept, one to refuse) when edge cases matter.
- With thinking models, a worked example as problem, method, answer shapes how the model reasons about similar problems. (Anthropic)

## 6. Structure

- Separate instructions, context, examples and input with XML tags or headings, one scheme throughout.
- Long documents first, question and instructions last (Anthropic reports up to 30% better on multi-document tasks). For long inputs, ask for relevant quotes before the answer.
- Prompt style leaks into output style: a prompt with less markdown gets less markdown back.

## 7. Role: one functional line

"You are a contract lawyer reviewing a SaaS order form for a buyer" focuses tone and expertise. A long persona adds nothing; expertise shows in the instructions. (Anthropic, Google p.21-23)

## 8. Ask first on triggers

For ambiguous or high-stakes work, tell the model not to start yet: it lists what is missing and asks. Otherwise let it state an assumption in one line and proceed. Asking costs a turn; guessing wrong costs a rework round. (Prompt Optimization Guide, Mastering Claude AI Ch.4)

## 9. Length and verbosity

State the length you want. Default length differs by model (Opus 5 writes longer user-facing answers; effort does not reliably shorten them), so a length line beats relying on defaults. (Anthropic)

## 10. Iterate, one thing at a time

Attempt, look at what is missing, refine. Ship a rough first prompt and improve it rather than polishing it blind.

## Five pitfalls (Mastering Claude AI Ch.4)

1. **Kitchen sink:** write, edit, format and optimise in one ask. Split into steps.
2. **Mind reader:** assuming intent is obvious. State it.
3. **One size fits all:** the same template for code and for prose. Adapt.
4. **Perfectionist paralysis:** polishing prompt one forever. Draft and iterate.
5. **Over-constraining:** stacked criteria that conflict. Keep the relevant ones.

## Pre-send checklist

- [ ] Context and intent stated (what for, who reads it)
- [ ] Task specific; "done when" clear
- [ ] Format and length stated
- [ ] Reasons given for non-obvious rules; no capitals for emphasis
- [ ] Would one example say it faster than more description?
- [ ] Long material above the question
- [ ] One thing at a time

See also: [[advanced|Advanced Techniques]], [[model-choice-and-effort|Model Choice and Effort]], [[retired|Retired Techniques]].
