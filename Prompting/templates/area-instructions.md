---
title: "Template: Area Instructions (AGENTS.md / CLAUDE.md)"
---

Instructions for any agent working inside one area: a repo, a folder, a vault, a tool or an account. Built from [[../guidelines/system-prompt-guidelines|the guidelines]], sections 4, 5 and 6.2. Target: under 200 lines.

**How to use:** fill `AGENTS.md` from the first block and create `CLAUDE.md` from the second so Claude Code imports it. Delete sections that do not apply and all `<!-- -->` comments. Start small: add a rule when an agent makes the same mistake twice.

## `AGENTS.md`

```markdown
# [Area name]

<!-- 1-2 lines: what this area is and what agents usually do here. -->
[What this is, e.g. "Personal Obsidian vault: notes, not code. Agents mostly search, write and reorganise notes."]

<!-- Where things live. Link to the spec if one exists; do not paste it. -->
## Map
| Path | Holds |
|---|---|
| `[path/]` | [what belongs there] |
Placement rules: see `[path/to/spec]`. If an item fits nowhere, put it in `[inbox path]` and ask.

<!-- Only commands an agent would otherwise guess wrong. -->
## Commands
- Search: `[command]` ([why this over the obvious alternative]).
- Test / build / lint: `[command]`.
- Move or rename: `[command]`, because [reason, e.g. "it rewrites links; plain mv breaks them"].

<!-- Conventions an agent would not infer. Each with a short reason. -->
## Conventions
- [Naming rule], because [reason]. Full rules: `[link]`.
- [Format rule, e.g. "every note starts with YAML frontmatter"], because [reason].

<!-- Draw the line by reversibility. Reasons keep rules from being applied too rigidly. -->
## Boundaries
**Go ahead:** [read, search, draft, edit files you created in this task].
**Ask first:** [moves, deletes, bulk edits, anything published or sent, changes to shared config], because [reason].
**Never:** [e.g. "touch `.obsidian/` or `[protected path]`"; "write credentials into files"], because [reason].

<!-- The contract part. Each risky action produces visible output before it happens. -->
## Before risky actions
Before [creating, moving or deleting files], output:
    RULE: <which rule in [spec] applies>
    DEST: <destination derived from that rule>
    IMPACT: <e.g. number of inbound links, with the command used>
Then stop and wait for confirmation. If you cannot fill these lines from the spec, ask instead.

## Reporting
Skipped steps first, then: done / also done unasked / needs my decision. Numbers carry the command that produced them.

<!-- Links, not copies. -->
## References
- [Spec or style guide]: `[path]`
- [Runbook]: `[path]`
```

## `CLAUDE.md` (thin pointer)

```markdown
# [Area name]: Claude Code entrypoint

The canonical instructions for this area are in [AGENTS.md](./AGENTS.md).
Edit AGENTS.md, not this file.

@AGENTS.md

<!-- Only genuinely Claude-specific additions below (skill names, hooks). Never restate AGENTS.md. -->
```

## Notes

- **Sub-areas:** add a nested `AGENTS.md` only where rules truly differ. The nearest file wins; do not repeat parent rules.
- **Hard limits:** prose is context, not enforcement. Back up each "never" with a permission rule or hook where the tool supports it.
- **Other tools:** Gemini CLI can be configured to read `AGENTS.md` (`context.fileName` in settings); Cursor reads `AGENTS.md` or `.cursor/rules/*.mdc`.
- **Code repo variant:** for a product repo, add "Verifying your work" (exact build, test, lint and eval commands, with evidence required), "Working from a plan" (follow the approved plan, record deviations), and "Protected paths" (also enforced by a hook). My AI-Native SDLC templates (private vault, `JB/Frameworks/AI-Native-SDLC/`) contain this variant.
- **Obsidian vault variant:** `System/Templates/AI Guideline Template.md` is a Templater version of this template for per-scope guideline notes inside the vault.
