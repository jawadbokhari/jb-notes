---
title: What is a Skill?
parent: AI Fundamentals
permalink: /ai-fundamentals/what-is-a-skill/
---

## What is a Skill?
A skill as a **self-contained capability bundle** — everything an agent needs to perform a specific function, packaged together.
At the simplest level a Skill is something you enable your AI agent to do some work. 

| Component     | Example                                                       |
| ------------- | ------------------------------------------------------------- |
| Knowledge     | Domain context, reference docs, guidelines                    |
| Scripts       | Python/bash scripts the agent can execute                     |
| Tools         | Functions the LLM can call (e.g., search, calculator)         |
| MCPs          | Model Context Protocol servers exposing external capabilities |
| Prompts       | System instructions scoped to that capability                 |
| Config/Schema | How to invoke the skill, expected inputs/outputs              |

### Built-in LLM Capabilities (not "Skills"):
These are emergent abilities an LLM develops during training — not "skills" in the packaged sense:
- summarizing text
- writing code
- translating language
- reasoning through problems

> Skills in Claude Code are **explicit, packaged instruction files** that extend or guide these built-in capabilities. Don't confuse the two.

### Explicit (Packaged) Skills:
> A set of instructions that tell the model (LLM) how to do something. 

- Available Skills: 
	- Run `/skills` on `claude` CLI 
	- On Claude.ai, you can find them in Customize > Skills
- Loading: 
	- On the agent start-up, all given skills are loaded (only metadata name+description from YAML frontmatter)
	- Full skill body and resources are loaded when the agent invokes the skill. 
- Invoking Skills: 
	- on direct calling with skill-name with a slash command, e.g., `/review`
	- or matching user prompt with the skill description (yaml frontmatter)
- Definition: Skills creation follow standard defined in https://agentskills.io/
	- A Skill file should be less than 500 words
	- A skill name must be less than 64 characters
	- A skill name should be descriptive and action-oriented (e.g., `simplify`, `review-pr`, `generate-doc`). No single strict convention — clarity and intent matter most.
- Skill Levels: Skills exist at three levels.  enterprise, user, and project - enterprise take precedence
	- Enterprise - Managed via API / org policy, have the highest priority
	- User - saved in `~/.claude/skills/` and have medium priority
	- Skills at the project level are shared with teammates through source control

> **Example**
> Anthropic Frontend Design Skill https://claude.com/blog/improving-frontend-design-through-skills#real-world-skills-examples

## Skill Distribution
Organizations such as Anthropic, Figma, and many others have published their skills for download. 
### Communities 
Download as an archive and keep it in your user or project for use. 
- https://skillsmp.com/
- SkillHub

### Organizational 
- Create Skill git repositories.  Collaborators can review and improve skills. 
Distribute via [Plugins & Marketplaces](/jb-notes/ai-fundamentals/plugins-and-marketplaces/). Company-wide git repositories can definitely be published as an internal marketplace.

### Your Skills 
You can create your skill repository and share with the world.

## Loading and Using Skills

### on Claude Code
```sh
# browse all available plugins
/plugin

# add a plugins on claude-code
/plugin marketplace add owner/repo

# install one using command or make a choice on marketplace
/plugin install document-skills@anthropic-agent-skills
```


> Use **OpenSkills** CLI to install Anthropic skills to other AI agents such as Cursor, Co-pilot, etc.

