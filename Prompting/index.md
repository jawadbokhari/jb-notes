---
title: Prompting (workspace)
---

Working notes for learning and practicing prompt engineering (model-agnostic, with Claude-specific notes). Not published: see `AGENTS.md` for the staging to `content/prompting/` publish workflow.

## Start here
- [[guidelines/system-prompt-guidelines|System Prompt Guidelines]]: how to write standing instructions at user, area and agent level, contract principles, outdated advice, and review checklists

## Instruction templates (standing instructions)
- [[templates/user-system-prompt|User System Prompt]]: how any AI should work with me, portable across tools
- [[templates/area-instructions|Area Instructions]]: `AGENTS.md` plus the thin `CLAUDE.md` pointer, for a repo, folder, tool or account
- [[templates/agent-contract|Agent Contract]]: a new agent or sub-agent, with inputs, tools, autonomy, checkpoints, stop conditions, output and definition of done
- [[templates/task-workflow|Task Workflow]]: lightweight procedure for one repeatable task

## One-off prompt templates
- [[templates/one-off/universal|Universal]]: master prompt template, problem-solving framework
- [[templates/one-off/business|Business]]: executive summary, SWOT, meeting agenda
- [[templates/one-off/writing|Writing]]: blog post blueprint, email enhancement
- [[templates/one-off/learning|Learning]]: concept mastery, study guide
- [[templates/one-off/creative|Creative]]: story development, brainstorming
- [[templates/one-off/research|Research]]: CRAAP source analysis, research synthesis matrix, persona behaviour and scenario extraction
- [[templates/one-off/data-and-productivity|Data & Productivity]]: quick data story, morning briefing, weekly review
- [[templates/one-off/meta-prompting|Meta-prompting]]: ask what's missing, draft, improve, conflict check, diagnose a failure, test cases, conversation to prompt, port to another model

## Techniques
- [[techniques/foundational|Foundational Prompting Techniques]]: anatomy (context, intent, task, format, constraints, done when), reasons with rules, literal scope, examples, structure, one-line role, ask on triggers, pitfalls, pre-send checklist
- [[techniques/advanced|Advanced Prompting Techniques]]: draft-critique-revise, adversarial review, multi-perspective, rubrics, step-back, meta-prompting, evals, constraint engineering, long agent runs, which technique when
- [[techniques/model-choice-and-effort|Model Choice and Effort]]: which model and effort to give a task, escalation order, subagent model rules
- [[techniques/retired|Retired and Downgraded Techniques]]: what no longer pays off on reasoning models (written chain of thought, prefill, recursive CoT, quotas) and what replaces it

## Sources
Each source note carries `source_type`, `currency` (current, partly-dated, dated) and `reviewed` in its frontmatter. Partly-dated notes open with a currency line saying what still holds.

**Vendor documentation (current)**
- [[sources/vendor-guidance-2026|Vendor Guidance on System Prompts and Agents]]: Anthropic (incl. Claude 5 model, effort and thinking guidance, checked 2026-11-07), OpenAI, Google, AGENTS.md, Cursor; re-check when models change

**Practitioner guides and articles**
- [[sources/anthropic-which-claude-model|Which Claude Model Should You Build With? (Anthropic, 2026-11)]] (current): task-to-model table, prices, effort curve, mixing models, migration checks
- [[sources/prompt-optimization-guide|Prompt Optimization Guide]] (current): fix the prompt first, nine optimisation techniques, model escalation
- [[sources/ai-agent-system-instructions|AI Agent System Instructions (Dust Blog + Claude Code Tutorial)]] (partly dated): three-layer model, six-part anatomy, three-tier guardrails
- [[sources/agent-autocorrect-and-workflow-files|Agent Auto-Correction & Workflow Files (Claude Code Tutorial)]] (partly dated): plan-first, four-pillar Workflow File

**Books, papers and courses**
- [[sources/google-prompt-engineering-whitepaper|Prompt Engineering Whitepaper (Google, Lee Boonstra, 2024)]] (partly dated): best practices still hold; reasoning and sampling sections retired
- [[sources/mastering-claude-ai|Mastering Claude AI (Ryan Dickey, 2025)]] (partly dated): prompt anatomy, pitfalls, advanced strategies, one-off templates
- [[sources/anthropic-prompt-engineering-interactive-tutorial|Anthropic Prompt Engineering Interactive Tutorial]] (dated): first course, Claude 3 era

## Resources
- [[prompt-and-skill-libraries|Prompt and Skill Libraries]]: official and community prompt and skill collections, with vetted status

## Workspace
- [[currency-review-2026-11-07|Currency review against Claude 5 family docs (2026-11-07)]]
- [[restructure-task-list|Task list: guidelines and templates restructure (2026-09-25)]]
