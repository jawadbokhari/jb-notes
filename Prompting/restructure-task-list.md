---
title: "Task List: System Prompt Guidelines and Templates"
---

Tracks the 2026-09-25 restructure of this workspace into guidelines plus templates. Goal: (1) guidelines for system prompts and contract-style agent instructions, (2) a user-level system prompt template, (3) agent contract templates for `AGENTS.md` / `CLAUDE.md` style agent and sub-agent definitions. Decisions: home is `jb-notes/Prompting/`; model-agnostic with Claude-specific notes; three levels (user, area, agent).

## Phase 1: Sources
- [ ] 1.1 Research current vendor guidance (Anthropic, OpenAI, Google, AGENTS.md) via research sub-agent
- [ ] 1.2 Condense research into `sources/vendor-guidance-2026.md`
- [x] 1.3 Extract Google whitepaper into `sources/google-prompt-engineering-whitepaper.md`
- [ ] 1.4 Review both source notes for accuracy and style (no em dashes, citations present)

## Phase 2: Guidelines
- [ ] 2.1 Write `guidelines/system-prompt-guidelines.md`: shared core, user level, area level, agent contract level
- [ ] 2.2 Fold in drift case study guardrails (G1 to G8) as contract principles, linked not copied
- [ ] 2.3 Replace dated advice (fixed clarifying-question count, emphatic caps, rules without reasons)
- [ ] 2.4 Add a review checklist per level

## Phase 3: Templates
- [ ] 3.1 `templates/user-system-prompt.md`
- [ ] 3.2 `templates/area-instructions.md` (AGENTS.md / CLAUDE.md for a repo, folder or tool)
- [ ] 3.3 `templates/agent-contract.md` (agent and sub-agent, with optional handoff section)
- [ ] 3.4 `templates/task-workflow.md` (lightweight SOP, from the old Workflow File)
- [ ] 3.5 Retire `templates/system-instructions.md` once its content is carried over

## Phase 4: Validation
- [ ] 4.1 Draft user-level prompt from `JB/Prompt-Library/JB-as-a-Senior-Product-Leader-System-Prompt.md` using 3.1 (new draft, original untouched)
- [ ] 4.2 Draft agent contract from `JB/Prompt-Library/Expert-Work-Organizer.md` using 3.3 (new draft, original untouched)
- [ ] 4.3 Record template gaps found, fix templates

## Phase 5: Organize and link
- [ ] 5.1 Link check and dry run for moves (one-off templates into `templates/one-off/`), get confirmation
- [ ] 5.2 Move with `obsidian move`
- [ ] 5.3 Update `index.md` and `AGENTS.md` (structure, sources logged)
- [ ] 5.4 Align `System/Templates/AI Guideline Template.md` with the area-level template
- [ ] 5.5 Add `template:` property to Prompt-Library notes
- [ ] 5.6 Final check: links resolve, no em dashes in new files, git status reviewed
