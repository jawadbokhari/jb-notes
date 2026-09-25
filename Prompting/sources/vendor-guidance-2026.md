---
title: "Source: Vendor Guidance on System Prompts and Agents (2026 scan)"
---

Condensed from a sourced desk-research pass run 2026-09-25 across official Anthropic, OpenAI and Google documentation, the AGENTS.md open format, Cursor rules, and one practitioner source. All URLs accessed 2026-09-25. Type tags: **[doc]** official product doc, **[blog]** official engineering blog, **[prac]** practitioner (secondary).

## Anthropic (Claude)

**Prompting best practices** [doc] `platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices`
- Golden rule: show the prompt to a colleague with minimal context. If they would be confused, the model will be too.
- Give the reason behind a rule. Bare `NEVER use ellipses` is weaker than explaining the output is read by a text-to-speech engine. "Claude is smart enough to generalize from the explanation."
- Say what to do, not what to avoid ("write flowing prose paragraphs" beats "do not use markdown").
- **Dial back emphasis.** Current models are more responsive to the system prompt; `CRITICAL: You MUST use this tool when...` now overtriggers. Use "Use this tool when...". Prompts written to push older models harder should be toned down.
- Role: one sentence focuses behaviour and tone. No elaborate persona needed.
- Examples: 3 to 5, in `<example>` tags, diverse so unintended patterns are not copied.
- Structure with XML tags (`<instructions>`, `<context>`, `<input>`), consistent names.
- Long inputs at the top, question and instructions at the end (up to 30% better on multi-document tasks). Ask for relevant quotes before answering.
- Action vs. suggestion: models follow wording precisely ("suggest changes" yields suggestions, not edits). Ship an explicit "default to action" or "do not act before instructions" line depending on the intent.
- Overengineering: models may add files, abstractions or flexibility not asked for. Scope them to what was requested or clearly necessary.
- Autonomy line drawn by **reversibility and blast radius**: act on local, reversible work; ask before destructive, hard-to-reverse, or shared/visible actions.
- Subagent overuse is a real failure mode. Delegate only genuinely parallel, isolated or independent work.

**Effective context engineering for AI agents** [blog, 2025-09-29] `anthropic.com/engineering/effective-context-engineering-for-ai-agents`
- "Find the smallest set of high-signal tokens that maximize the likelihood of your desired outcome."
- Right altitude: between brittle hard-coded logic and vague high-level guidance. Strong heuristics, sectioned with headers or tags.
- Start minimal on the best model, then add instructions only for observed failure modes.
- Tools: self-contained, unambiguous. If a human cannot say which tool fits a situation, the agent cannot either.
- Sub-agents return condensed summaries (about 1,000 to 2,000 tokens) to the coordinator, not transcripts. Load data just in time via identifiers rather than preloading.

**Building effective agents** [blog, 2024-12-19, older but still canonical] `anthropic.com/engineering/building-effective-agents`
- Workflows (predefined code paths) vs. agents (model directs its own steps). Use agents for open-ended work with clear success criteria and human oversight.
- Simplicity, transparency (show planning steps), and investment in tool documentation. Add complexity only when it measurably helps.

**Claude Code memory (CLAUDE.md)** [doc] `code.claude.com/docs/en/memory`
- CLAUDE.md is **context, not enforced configuration**. To block an action regardless of the model, use a hook or permission rule.
- Target under 200 lines per file; longer files reduce adherence. Move conditional content to path-scoped rules or skills.
- Concrete enough to verify: "Run npm test before committing", not "Test your changes".
- Add an entry when the same mistake happens twice, or a new teammate would need the same context.
- Contradictory rules get resolved arbitrarily. Prune them.
- Files load root to leaf and are concatenated. HTML comments are stripped before injection (free maintainer notes).

**Claude Code subagents** [doc] `code.claude.com/docs/en/sub-agents`
- Frontmatter: `name` and `description` required; `tools` (allowlist), `disallowedTools`, `model`, `maxTurns`, `memory`, `skills` optional.
- `description` drives delegation: say *when* to use it ("Use when...", "use proactively"). Detailed instructions go in the body.
- A subagent gets only its own prompt, the task message and the CLAUDE.md chain. **No parent conversation history.** Its prompt must be self-sufficient.
- Use subagents for verbose, self-contained or parallel work; keep iterative, context-heavy or latency-sensitive work in the main session.

**Skill authoring best practices** [doc] `platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices`
- Assume the model is already smart. Test each paragraph: does it justify its token cost?
- Match **degrees of freedom** to fragility: prose heuristics for judgment calls, parameterized patterns for preferred approaches, exact scripts for fragile operations.
- Descriptions in third person, stating what and when, with trigger terms.
- Body under 500 lines; references one level deep. No time-sensitive wording in the body.
- Build evaluations before extensive documentation: find real gaps first, then write the minimum to close them.

## OpenAI

**GPT-5.1 prompting guide** [doc] `developers.openai.com/cookbook/examples/gpt-5/gpt-5-1_prompting_guide`
- Pushes autonomy: "Persist until the task is fully handled end-to-end within the current turn whenever feasible." If the answer to "should we do X?" is yes, do X.
- Plan before tool calls, reflect after them.
- **Metaprompting** for conflicts: ask the model to find contradictory rules in your prompt, then make surgical edits. Typical conflicts: autonomy vs. clarification, brevity vs. completeness, tool thresholds vs. concision.
- Conditional verbosity budgets by task size instead of one blanket rule. Progress updates carry a concrete outcome, not just next steps.

**Model Spec** [doc] `github.com/openai/model_spec`
- Formal authority tiers: root > system > developer > user > guideline. Guidelines are soft defaults that yield to context.
- Follow the letter and spirit: models read intent, so state intent and the intended scope of autonomy.

**Agents SDK: handoffs and guardrails** [doc] `openai.github.io/openai-agents-python/`
- Describe handoffs in the agent's instructions; `handoff_description` is the short "when to hand off" line.
- Handoff payloads stay small (reason, priority, summary), not full history. Filter what the next agent sees.
- Guardrails at three points: input, output, and per tool. Tripwires halt deterministically. Handoffs bypass agent-level guards, so put guards on risky tools.

**A practical guide to building agents** [doc, lower confidence: PDF not parsed, landing page plus secondary summary]
- Start with one agent plus tools; split into multiple agents only when needed. Derive agent instructions from existing operating procedures.

**AGENTS.md** [open format] `agents.md`
- Plain Markdown, no required schema. "A README for agents": build and test commands, conventions, security notes, PR rules.
- Nearest file in the tree wins. Chat instructions override the file.
- Read by 30+ tools (Codex, Claude Code, Copilot, Cursor, Gemini CLI and others): the closest thing to a cross-vendor standard.

## Google (Gemini)

**Prompt design strategies** [doc] `ai.google.dev/gemini-api/docs/prompting-strategies`
- System instructions hold persona, role, constraints and output format; they persist across turns.
- Few-shot by default, 2 to 4 varied examples with identical formatting.
- Gemini 3: "Be precise and direct... Avoid unnecessary or overly persuasive language." Defaults to direct answers.
- Context first, instructions and question last. XML-style tags or Markdown headings, consistently.
- Agentic template: state risk tolerance for exploratory vs. state-changing actions, and how persistent to be on errors.

**Gemini CLI GEMINI.md** [doc] `github.com/google-gemini/gemini-cli/blob/main/docs/cli/gemini-md.md`
- Global, project and component files are all concatenated. Headings, bullets and short snippets parse most reliably.
- `@file.md` imports. Filename list is configurable, so Gemini CLI can read `AGENTS.md` as primary.

## Cursor

**Rules** [doc] `cursor.com/docs/rules`
- `.cursor/rules/*.mdc` with `description`, `globs`, `alwaysApply`. Under 500 lines.
- Reference files instead of copying them. Add rules only when the agent repeats a mistake.

## Practitioner

**12-Factor Agents** [prac] `github.com/humanlayer/12-factor-agents`
- Successful agents are mostly ordinary software with LLM calls at decision points. Own your prompts, context window and control flow.
- Small, focused agents. Contact humans through tool calls. Compact errors before feeding them back.

**Spec-driven development / agent contracts** [prac, under-verified]
- A spec should act as a validation gate: outcomes, scope, constraints, prior decisions, and verification criteria. No single canonical primary source found.

## Cross-vendor consensus

1. Give reasons; do not rely on bare prohibitions.
2. Say what to do rather than what to avoid.
3. Normal wording; capitals and "CRITICAL / MUST" now overtrigger.
4. Consistent structure with headers or XML tags.
5. Long context first, instructions last.
6. Few, diverse, consistently formatted examples.
7. Concrete, verifiable phrasing.
8. Area files short (under 200 to 500 lines), grown reactively, referencing rather than copying.
9. Hierarchical files concatenate; nearest file wins on conflict.
10. Write success and stop criteria into the instruction.
11. State autonomy explicitly and per task; reversibility is the practical line.
12. Short functional roles, not elaborate personas (inference from what vendors recommend, not an explicit rule).

**Vendor differences:** OpenAI leans toward autonomous completion, Anthropic documents both an "act" and an "ask" setting, Google asks for explicit risk tolerance. OpenAI alone publishes a formal authority hierarchy. Anthropic publishes per-model migration notes; check them when a model changes.
