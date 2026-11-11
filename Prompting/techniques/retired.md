---
title: Retired and Downgraded Techniques
reviewed: 2026-11-07
---

Techniques from older sources that no longer pay off on current reasoning models, and what to use instead. Checked against Anthropic's prompting docs on 2026-11-07; re-check when models change. Current techniques: [[foundational|Foundational]], [[advanced|Advanced]].

## Retired

| Technique | Found in | Why it no longer pays off | Use instead |
|---|---|---|---|
| "Let's think step by step" / manual chain of thought in the answer | Google p.29-31, Mastering Claude AI Ch.4 | Thinking is built in (always on for Fable 5.2 and Opus 5.5). Asking for written reasoning duplicates it and may be declined as reasoning extraction on Fable 5.2, Opus 5.5 and Sonnet 5.5 | Raise effort; ask for checkable artefacts (weakness list, rubric result) |
| "Think carefully before answering" in a chat system prompt | Common practice | On Opus 5.5 removing it made replies start sooner with no clear quality loss | Leave thinking to the model; use effort |
| Recursive chain of thought (five written levels), self-questioning cascade | Mastering Claude AI Ch.10 | Prescribes the thinking; "think thoroughly" often beats a hand-written reasoning plan, and errors compound across levels | Draft, critique, revise |
| Tree of thoughts as a prompt pattern | Google p.36 | Native thinking explores alternatives internally | For real breadth, run separate attempts or sub-agents and compare |
| Prefilled assistant response | Older Anthropic tutorials | Returns a 400 error on Claude 4.6 and later | Format instructions, structured outputs, examples |
| `budget_tokens` thinking budget | Older Anthropic API docs | Deprecated; a 400 error on Claude 4.7 and later | `effort`, with `max_tokens` as a hard limit |
| "CRITICAL: you MUST..." in capitals; "if in doubt, use [tool]" | Prompts written for older models | Current models over-apply them | Normal wording plus the reason |
| Hand-built ReAct loops (LangChain + search API) | Google p.37-39 | Superseded by native tool use and agent SDKs; the reason-act-observe idea stays | Native tool calling |
| Automatic prompt engineering scored with BLEU/ROUGE | Google p.40-41 | Surface metrics miss meaning | LLM-judged evals against your own criteria |
| Fixed clarifying-question counts ("ask at least three", "never more than two") | Agent tutorials, Prompt Optimization Guide | Asks when it should act, or stops short when it should ask | Ask on triggers (ambiguity, costly wrong guess, user's decision) |
| Long character personas, "you are a helpful assistant" | Many prompt libraries | Adds nothing or adds noise | One functional role line |
| Iteration scripts ("That's helpful! Now can you...") | Mastering Claude AI App. A | Politeness formulas carry no instruction | Say what to change and why |

## Downgraded (still valid in a narrow case)

| Technique | Narrow case where it still applies |
|---|---|
| Sampling settings tables (temperature, top-K, top-P) | Direct API work only; most chat and agent tools do not expose them. Not checked against current model docs |
| Self-consistency (many sampled runs, majority vote) | Batch API work with a single checkable answer; in chat, two or three runs to spot disagreement is enough |
| "Three to five examples minimum", "start with about six" | Classification and strict formats; elsewhere one or two varied examples often suffice |
| Manual chain of thought in `<answer>` tags | Older models with thinking turned off |
| Role prompting as the first fix for generic output | Still useful as one line; generic output usually means missing context or intent |
