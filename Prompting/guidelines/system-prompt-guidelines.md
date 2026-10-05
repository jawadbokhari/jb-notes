---
title: "Guidelines: System Prompts and Agent Contracts"
---

How to write standing instructions for AI: a personal system prompt, an area-level file (`AGENTS.md`, `CLAUDE.md`, `GEMINI.md`), and a contract for an agent or sub-agent. Model-agnostic, with vendor notes at the end. Templates that apply these rules live in `templates/`.

Sources: [[../sources/vendor-guidance-2026|Vendor Guidance 2026]], [[../sources/ai-agent-system-instructions|AI Agent System Instructions]], [[../sources/agent-autocorrect-and-workflow-files|Agent Auto-Correction & Workflow Files]], [[../sources/google-prompt-engineering-whitepaper|Google Prompt Engineering Whitepaper]], [[../sources/mastering-claude-ai|Mastering Claude AI]], and my own instruction-drift case study (private vault note, lessons summarised in section 5).

## 1. Pick the right artefact

| You want to...                                                        | Level          | Template                                                | Lives in                                                                                              |
| --------------------------------------------------------------------- | -------------- | ------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| Tell every AI how to work with *me*                                   | User           | [[../templates/user-system-prompt\|User System Prompt]] | `~/.claude/CLAUDE.md`, `~/.gemini/GEMINI.md`, ChatGPT custom instructions, Claude profile preferences |
| Tell any agent how to behave inside one repo, folder, tool or account | Area           | [[../templates/area-instructions\|Area Instructions]]   | `AGENTS.md` (canonical); `CLAUDE.md` only for Claude-only content                                         |
| Define a new agent or sub-agent with a job, tools and limits          | Agent          | [[../templates/agent-contract\|Agent Contract]]         | `.claude/agents/<name>.md`, an agent's own `AGENTS.md`, SDK `instructions`, a Gem or custom GPT       |
| Standardise one repeatable task an existing agent runs                | Task           | [[../templates/task-workflow\|Task Workflow]]           | a workflow file, skill or command                                                                     |
| Get one answer, once                                                  | One-off prompt | `templates/one-off/`                                    | the chat box                                                                                          |

Rule of thumb: if you would re-explain it next session, it is an instruction, not a prompt. If it has its own tools, scope and hand-back, it is an agent contract.

## 2. Vocabulary

- **Prompt**: a single request. Ends with the turn.
- **Instruction**: standing guidance loaded every session. Defines how the AI always operates.
- **Contract**: an instruction set for an agent that states obligations someone can *check*: what it receives, what it returns, what it may do alone, where it must stop, and how "done" is verified. A contract differs from ordinary instructions because each important rule produces something visible.

## 3. How the levels stack

```
User (me, everywhere)
  └─ Area (this repo / folder / tool)
       └─ Agent (this agent's job)
            └─ Task (this run)
```

- Files concatenate; the **nearest file wins** on style and format conflicts (Claude Code, Gemini CLI and AGENTS.md all work this way).
- Safety, privacy and data-boundary rules set at the user level are not overridden lower down. Say so explicitly in the user-level file.
- **One home per rule.** Put a rule at the highest level where it is always true, and nowhere else. Copies drift into different versions.
- **Sub-agents inherit nothing from the parent conversation.** In Claude Code a sub-agent sees its own prompt, the task message and the area files, not the chat history. Write agent contracts to stand alone.
- Instruction files are context, not enforcement. Anything that must never happen belongs in a hook, permission rule or tool guardrail as well as in prose.

## 4. Core principles (all levels)

1. **Write for a smart newcomer.** If a capable colleague with no context would be confused, so will the model. Assume competence; do not explain what the model already knows.
2. **Give the reason with the rule.** One clause is enough: "No ellipses, because output is read by a text-to-speech engine." Models generalise from the reason to cases the rule did not list. Style bans (em dashes, tone, greetings) need a reason too, or they look arbitrary and get dropped.
3. **Say what to do.** Positive instructions beat lists of prohibitions. Keep "never" for safety and irreversible actions.
4. **Use normal emphasis.** Capitals, "CRITICAL" and "You MUST" cause current models to over-apply a rule. If everything is urgent, nothing is.
5. **Be concrete enough to verify.** "Run the tests before committing", not "make sure it works". If you cannot tell whether a rule was followed, rewrite it. Vague wishes ("keep it brief") become a default you can check ("answer in the first sentence; about 150 words unless I ask for more"). Mark numbers you chose as estimates.
6. **Start minimal, grow on evidence.** Add a rule when the same mistake happens twice, not for imagined cases. Budgets: user file about 30 to 80 lines, area file under 200, agent contract under 500.
7. **Rules in the file, history elsewhere.** A short reason belongs with the rule. Rationale essays, change logs and post-mortems go in a separate note. Narrative in a spec invites narrative in the output.
8. **Structure consistently.** Markdown headings or XML tags, the same scheme throughout. When a prompt carries long material, put the material first and the instructions last.
9. **Examples: few, varied, labelled.** Two to five, differing in content but identical in format, marked as illustrations so they are not copied literally.
10. **Set autonomy by reversibility, not by task type.** Reversible, local work: proceed. Destructive, hard to undo, visible to others, or spending money: ask first. State this line explicitly; vendors disagree on the default.
11. **Ask on triggers, not quotas.** Replace "always ask three questions" with conditions: ask when a decision is the user's to make, when intent is ambiguous, or when a wrong guess is costly. Otherwise pick a sensible default and state the assumption.
12. **No contradictions.** Conflicting rules get resolved arbitrarily. Periodically ask a model to list conflicting or redundant lines in your file, then fix them surgically. Typical conflicts: brevity vs. completeness, autonomy vs. asking first.
13. **Keep it timeless.** No point-in-time state (current members, open tickets, today's config) in standing instructions. Point to where the live data is.
14. **Version and re-test.** Keep a short change log outside the file, and re-read the file when you switch models. Advice written to push an older model can overshoot on a newer one.

## 5. Contract principles (agents and area files)

The core lesson from my instruction-drift case study: **instruction text does not produce compliance; required output does.** A rule the AI can skip silently will eventually be skipped. A rule that must produce a visible artefact before the next step cannot be.

1. **Required checkpoint output.** For each high-stakes rule, name the output that proves it was applied (for example, a three-line preamble stating which rule applies and where the file will go). If the agent cannot produce it, it stops and asks.
2. **Gate irreversible actions.** Before a move, delete, send or deploy: show what will change, then stop and wait. Checks run after an action only tell you what broke.
3. **Definition of done.** List the checks that make the output acceptable. The agent runs them and reports the results before it claims completion.
4. **Explicit stop and escalate conditions.** Missing input, a failed tool, a conflicting rule, going outside its scope: say what the agent does in each case (stop, ask, report), not "use judgment".
5. **Evidence for claims.** Every number comes with the command or source that produced it. "X will happen" needs evidence; otherwise say "I expect X because Y". Where a record and the primary source disagree, the primary source wins.
6. **Declare scope expansion.** Anything done beyond the request is listed separately ("Also did, unasked"). This keeps useful initiative without hiding it.
7. **Fixed report shape, with a trigger.** Skipped or failed / done / also did unasked / needs your decision, skipped steps first. Apply it only after multi-step or file-changing work, show only non-empty parts, keep "done" to one line and do not restate what the diff shows. Without a trigger and a cap, the shape fights the brevity rule.
8. **Challenge the diagnosis.** When an agent explains its own failure, first ask whether the instruction was already in its context. Do not fix a compliance failure by adding more instruction text; add a required output or a hard control instead.
9. **Enforce outside the prompt where it matters.** Tool allowlists, permission rules, hooks, turn limits and guardrails do not depend on the model's attention.

## 6. Level-specific guidance

### 6.1 User level (my standing preferences)

- **Contains:** who I am in two or three lines, the domains I work across and the boundaries between them, how to communicate with me, the default autonomy line, how to handle uncertainty, and the report shape I want.
- **Leaves out:** project facts, current goals that change each quarter, long biographies, tool-specific mechanics. Those belong in area files or memory.
- **About me, not a persona for the AI.** Describe the user and the working relationship. Keep any role for the assistant to one functional line.
- **Portable core.** Write it once in plain Markdown so the same text works in Claude, ChatGPT and Gemini. Add tool-specific notes as a clearly separate tail section. Keep tool rules in the core at goal level ("GitLab: `glab` CLI only"); put mechanics (server names, script paths, failure workarounds, commands) in the tool's own file.

### 6.2 Area level (`AGENTS.md` / `CLAUDE.md`)

- `AGENTS.md` is the canonical file because 30+ tools read it. Claude Code can read it natively (setting `agents-md@builtin` = `claude-md-and-agents-md`), so add no `CLAUDE.md` pointer. Add a `CLAUDE.md` only for content that is truly Claude-only, and never restate `AGENTS.md` in it. Where a tool cannot read `AGENTS.md` natively, a thin `CLAUDE.md` containing `@AGENTS.md` is the fallback.
- **Contains:** purpose in one or two lines, where things live, the commands that matter, conventions with reasons, the act / ask first / never boundaries, required checkpoints for risky actions, and links to longer references.
- **Reference, do not copy.** Link to specs, style guides and runbooks instead of pasting them in.
- **Nearest file wins.** Put sub-area files only where rules genuinely differ; each rule has one home.
- Use path-scoped rules or skills for content that only matters sometimes, so the always-loaded file stays short.

### 6.3 Agent contract (agents and sub-agents)

- **Delegation description first.** One or two sentences in the third person saying what the agent does and *when* to use it, with trigger words. This is what an orchestrator reads to decide whether to call it.
- **Role in one sentence, mission in one more.** Expertise shows in the rules, not in adjectives.
- **Inputs:** what the agent receives, and what it does if something is missing.
- **Scope:** in scope and explicitly out of scope, so it does not wander.
- **Tools:** an allowlist, with when to use each. If you cannot say which tool fits a situation, the agent cannot either.
- **Process:** number the steps only where order matters. Match the degree of freedom to how fragile the step is: heuristics for judgment, exact commands for fragile operations.
- **Autonomy tiers** (act / ask first / never), each with its reason.
- **Stop and escalate conditions** and **required checkpoints** (section 5).
- **Output contract:** return format, length budget, and the fixed report shape. A sub-agent returns a condensed summary, not a transcript.
- **Definition of done:** the checks it runs before reporting completion.
- **Self-sufficient:** no reliance on the parent's conversation. Pass in, or tell it how to fetch, everything it needs.
- **Prefer fewer, focused agents.** Start with one agent and tools; split only when work is genuinely parallel or needs isolated context.

## 7. Outdated advice and what replaces it

| Common advice | Problem now | Use instead |
|---|---|---|
| "CRITICAL: you MUST..." in capitals | Over-applies on current models | Normal wording plus the reason |
| "You are a helpful assistant" / long character persona | Adds nothing, or adds noise | One functional role line; expertise shown through rules |
| "Always ask at least three clarifying questions" | Asks when it should act, stalls simple tasks | Ask on stated triggers; otherwise assume and state it |
| Bare "NEVER X" lists | Rigid, does not generalise | "Do Y, because Z"; keep "never" for safety |
| "Read the spec before acting" | Silently skipped | Require output that proves the spec was used |
| Fixing a missed rule by adding more rules | Longer file, lower adherence | A required checkpoint, a hook, or deleting a conflicting rule |
| Copying rules into every sub-folder file | Copies drift apart | One home per rule, nearest file wins |
| Current state in the instructions (members, tickets, configs) | Stale within days | Point to the live source |
| "Let's think step by step" everywhere | Built-in reasoning makes it redundant | Ask for a plan or visible reasoning only where you will check it |

## 8. Review checklists

Use before publishing or changing a file. Tick manually.

**All levels**
- [ ] A capable newcomer could follow it without asking me anything
- [ ] Every rule is concrete enough to check
- [ ] Rules carry a short reason; no essays, no change log inside
- [ ] No capitals or "CRITICAL" emphasis; "never" used only for safety or irreversible actions
- [ ] No contradictions (ask a model to list conflicts)
- [ ] No point-in-time state
- [ ] Each rule has one home; nothing duplicated from a higher level
- [ ] Within the length budget

**User level**
- [ ] Describes me and the working relationship, not an AI persona
- [ ] Autonomy line stated (act vs. ask first)
- [ ] Domain boundaries stated, marked as not overridable
- [ ] Tool-specific notes kept in a separate section

**Area level**
- [ ] `AGENTS.md` is canonical; any `CLAUDE.md` holds only Claude-only content
- [ ] Commands and locations are current and verifiable
- [ ] Risky actions have a required checkpoint
- [ ] Long material is linked, not pasted

**Agent contract**
- [ ] Description says what and when, in the third person
- [ ] Inputs, scope, out-of-scope stated
- [ ] Tools are an allowlist with when-to-use notes
- [ ] Stop and escalate conditions cover missing input, tool failure, conflict, out of scope
- [ ] Output contract and definition of done are checkable
- [ ] Works without the parent conversation
- [ ] Hard limits also enforced outside the prompt (tools, permissions, hooks, turn limit)

## 9. Vendor notes

- **Claude.** Most responsive to the system prompt of the three; tone down emphasis written for older models. XML tags work well. Claude Code: `CLAUDE.md` under 200 lines, HTML comments are stripped (free notes to maintainers), sub-agents defined in `.claude/agents/*.md` with `name`, `description`, `tools`, `model`. Check Anthropic's per-model migration notes when switching models.
- **OpenAI.** Defaults toward finishing the task end to end without pausing; if you want confirmation steps, say so explicitly. Formal authority order: platform > developer > user. Agents SDK uses `instructions`, `handoff_description`, and input, output and tool guardrails. Reads `AGENTS.md` (Codex).
- **Gemini.** "Avoid overly persuasive language." Few-shot examples by default. Context first, question last. Gemini CLI concatenates global, project and component `GEMINI.md` files and can be configured to read `AGENTS.md`.
