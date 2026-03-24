# Skills
A skill is a set of instructions based on the standard https://agentskills.io/. 
- Loaded on-demand based on direct calling with skill-name or prompt matching skill description
- A Skill file should be less than 500 words
- A skill name must be less than 64 characters
- A skill name should conventionally be verb-ing centric, e.g., testing-code, analyzing-pr, generating-doc, etc.
- Skills may exist at multiple levels: enterprise, user, and project - enterprise take precedence
## Skill Repositories
- Skills should definitely be shared across via Skill Git repositories. Collaborators can review and improve skills. 
- Ready to use skills may be distributed in [[#Plugins]] via marketplaces . Company-wide git repositories can definitely be published as an internal marketplace.

# Agents
Agents defined in .cursor/agents or .claude/agents are sub-agents that that runs like a forked-child process. It has its own execution context, though it loads context from the thread it was spawn off. 
> A sub-agent is an AI specialist of its kind that can independently do its job in isolation provided it's given the context and tools access in needs. 

Agent names follow a persona driven naming such as pr-reviewer.md, security-auditor.md, etc.

# Skills vs Agents
| **Feature** | **Skill (`SKILL.md`)**                                         | **Agent / Subagent (`.md`)**                                 |
| ----------- | -------------------------------------------------------------- | ------------------------------------------------------------ |
| Concept     | The "Manual": A specific playbook or set of instructions.      | The "Worker": An autonomous entity that performs a task.     |
| Context     | Shared: Injected into your current chat; uses the same memory. | Isolated: Runs in a separate "sandbox" to save tokens/noise. |
| Execution   | Passive: It gives the AI "knowledge" on how to do a task.      | Active: It takes over, runs commands, and returns a result.  |
| Trigger     | Automatic: Loaded when the AI detects it needs that expertise. | Delegated: The main AI "spawns" it to handle a sub-task.     |
| Best For    | Coding standards, API docs, or repetitive "how-to" steps.      | Complex research, long-running tests, or security audits.    |
| Analogy     | A YouTube Tutorial on how to fix a leaky pipe.                 | A Plumber you hire to actually fix the leak for you.         |

# Hooks
Hooks are automated injections triggered on defined events. For example, before making a tool, after writing a document, etc. Hooks are used for: 
- Deterministic actions: Always perform an action when something or some work is completed. For example, run tests on code commit, or run a security scan before submitting the pr
- workflow actions: Connect multiple actions in a workflow using hooks. For example, send a Google chat notification once PR-reviewer has completed the review.
- guardrails - check before a tool call that no harmful, dangerous action is going to happen. 

## Common Hook Events

| Event | When it Fires | Typical Use Case |
| :--- | :--- | :--- |
| **SessionStart** | When you first launch the assistant. | **Setup**: Pulling the latest Jira tickets or bug reports to prime the AI. |
| **UserPromptSubmit** | Immediately after you hit enter on a prompt. | **Context**: Injecting the current time or recent git status into the prompt. |
| **PreToolUse** | Before the AI runs any tool (e.g., `bash`, `write_file`). | **Blocking**: Checking for hardcoded secrets before saving. |
| **PostToolUse** | After a tool call succeeds. | **Cleanup**: Auto-formatting code with Prettier/Black after an edit. |
| **Notification** | When the AI needs your attention (e.g., for a permission). | **Alerts**: Sending a desktop notification so you can switch back to the terminal. |

# Plugins
A plugin is a package distributed via marketplace. A plugin is a container of skills, agents, rules, mcp servers, and hooks. Plugins are versioned and distributes via marketplaces. 
## Marketplace
A marketplace is where the plugins are available to download. These are public/private git repositories created following a defined marketplace repository structure. See [claude plugin-marketplaces](https://code.claude.com/docs/en/plugin-marketplaces) to create a plugin marketplace and [cursor marketplace](https://cursor.com/marketplace)for how companies have hosted their plugins on cursor marketplace.

