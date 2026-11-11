---
title: "Currency Review: Prompting Workspace (2026-11-07)"
---

Adversarial review of this workspace against Anthropic's prompting docs for the Claude 5 family (accessed 2026-11-07), triggered by the [[sources/prompt-optimization-guide|Prompt Optimization Guide]]. Question asked of every note: does this still change outcomes on current reasoning models, or does it now waste tokens or backfire?

## Findings

| Note | Finding | Action |
|---|---|---|
| `techniques/foundational` | Taught manual chain of thought; built on one book; no intent, literal-scope or length guidance | Rewritten as a multi-source synthesis |
| `techniques/advanced` | Centred on recursive chain of thought ladders, which prescribe thinking that models now do internally | Rewritten around artefact-producing review techniques |
| `guidelines/system-prompt-guidelines` | Already current on emphasis, quotas and personas; silent on effort, always-on thinking and reasoning-extraction refusals | Three rows added to the outdated-advice table; Claude vendor note updated |
| `sources/google-prompt-engineering-whitepaper` | Reasoning, ReAct, APE and sampling sections dated; best practices hold | Currency line added |
| `sources/mastering-claude-ai` | Chain of thought and iteration formulas dated; anatomy and pitfalls hold | Currency line added |
| `sources/ai-agent-system-instructions`, `sources/agent-autocorrect-and-workflow-files` | "Always ask three questions" and "always plan" quotas | Currency lines point to trigger-based asking |
| `sources/anthropic-prompt-engineering-interactive-tutorial` | Claude 3 era; relies on prefill and written reasoning | Marked dated; distillation dropped |
| `sources/prompt-optimization-guide` | Model claims mostly confirmed; "Fable is opt-in" unverified; "never more than two questions" is a quota | Verification table added |
| `templates/one-off/universal` | No purpose or done-when line | Both added |

## Not changed

- Other one-off templates (`business`, `writing`, `learning`, `creative`, `research`, `data-and-productivity`): structuring prompts with no retired technique found by a scan for chain-of-thought, persona and emphasis patterns. Not read line by line.
- Standing-instruction templates: they follow the guidelines, which needed only additions.
- Sampling-settings guidance: not checked against current model docs.
