---
title: BMad Best Practices
---

## What is BMad
[BMAD-METHOD](https://github.com/bmad-code-org/BMAD-METHOD) is an agent framework for structured product/dev work — a set of personas (analyst, PM, architect, dev, test architect, UX designer, …) each packaged as a skill/agent, plus workflows that chain them: brainstorm → PRD → architecture → epics/stories → dev → review.

It installs as `_bmad/` (source config + modules) compiled into `.agents/skills/` and `.claude/skills/` (the invokable skills).

## One install, used across projects
BMad doesn't need to live inside every project. It lives once at `~/ai/bmad` as its own repo and is invoked *against* whichever project you're working on — open a session there instead of installing a fresh copy per repo. Reasons:
- One canonical set of agents/skills instead of N copies drifting out of sync.
- Customizations (persona tweaks, custom modules) only need to be made once.
- Project repos stay lean — no `_bmad/` + duplicated skill folders bloating every clone.

> Keep genuinely **project-specific** skills (ones that only make sense for that one repo) in that project's own `.agents/skills/` — don't push those into the shared BMad repo. Only things that are reusable across projects belong centrally.

### Pointing BMad at a target repo
Because the install is standalone, `{project-root}` in `_bmad/config.toml` resolves to the BMad repo itself, not your target project. Before running a workflow against a specific repo, override the output/docs paths with that repo's **absolute path** in `_bmad/custom/config.user.toml` (personal, gitignored) — swap the block when you switch targets.

## The four-layer config
BMad merges config from four files, lowest to highest priority:
1. `_bmad/config.toml` — installer-managed, team. Regenerated on every install.
2. `_bmad/config.user.toml` — installer-managed, personal. Regenerated on every install.
3. `_bmad/custom/config.toml` — human-authored, committed, team-wide.
4. `_bmad/custom/config.user.toml` — human-authored, gitignored, personal.

**Rule of thumb:** never hand-edit files 1–2 for durable changes — the next install run overwrites them. Put durable overrides (agent persona tweaks, pinned paths, new agents) in `_bmad/custom/`, which the installer never touches.

## Modules
- **Stock** (reproducible from the public installer): `core`, `bmm` (product/dev — PM, architect, dev, analyst, UX), `cis` (creative — storytelling, brainstorming, innovation), `tea` (test architecture), `bmb` (BMad Builder — build your own agents/skills/modules).
- **Custom-built**: anything you or your team authored on top, e.g. a design-system module or a dev-loop automation module. Treat these as first-class — they don't come back from a reinstall, so back them up before ever re-running the installer.

## Typical workflow
| Stage | Skill/Agent | Output |
|---|---|---|
| Ideation | `bmad-brainstorming`, or talk to the Analyst | Sharpened problem framing |
| Requirements | `bmad-product-brief` → `bmad-prd` | Product brief, PRD |
| Design | `bmad-ux`, `bmad-architecture` | UX spec, architecture spine |
| Breakdown | `bmad-create-epics-and-stories` | Epics + stories |
| Build | `bmad-create-story` → `bmad-dev-story` | Implemented, tested story |
| Review | `bmad-code-review`, `bmad-testarch-*` | Findings, quality gate |

Don't know what to run next? `bmad-help` reads the current state and recommends the next skill instead of guessing.

## Practical tips
- Talk to agents by name once you know who does what (Mary = analyst, John = PM, Winston = architect, Amelia = dev, Sally = UX, Murat = test architect) — it's faster than describing the role every time.
- Use `bmad-party-mode` when you want multiple agent perspectives on the same question at once (e.g. PM + architect + dev sanity-checking a plan together) instead of running them serially.
- `bmad-advanced-elicitation` is the tool for "push back on this / stress-test this" — invoke it when an agent's output feels too agreeable.
- Route planning artifacts to where they actually belong in your project structure, not a generic dump folder — decide the routing convention once, per project, and document it so every future BMad session follows it automatically.
- Before letting the installer re-run to refresh stock modules, verify (dry-run / read release notes) that it won't clobber your custom modules or `_bmad/custom/` overrides, and back up `_bmad/` regardless.

## Related
- [[what-is-a-skill|What is a Skill?]]
- [[skills-vs-agents|Skills vs Agents]]
