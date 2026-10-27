---
title: Spec-Driven Communication
tags:
  - ai
  - spec-driven-development
  - coding-agents
---


When you hand a long task to an AI, it does not ask what you meant. It guesses, and you find out later. The fix is old and simple: agree on the work in writing before it starts, and decide in advance how you will know it is done. I learned a structured way to do that from a course for programmers, and I think it works for anyone who delegates to AI, whether the task is code, a report or fixing a deployment process.

Paul Everitt's [Spec-driven development with coding agents](https://www.deeplearning.ai/courses/spec-driven-development-with-coding-agents) (DeepLearning.AI with JetBrains) is an excellent beginner course on the fundamentals of spec-driven development. It is mainly about coding agents, but for me it unlocked something wider: how to build shared understanding with an AI so that I can delegate longer tasks to it with higher confidence.

In a nutshell, spec-driven communication is agreeing with an agent in writing, in layers from strategic to tactical: a spec for the intent, then for each phase, then for each task. Every spec states what I want, what is out of scope and how I will know it is done. Standing rules apply to all of it. I approve the criteria, and the agent's work is checked against them by a test or a separate reviewer. After each piece of work I update the specs and rules. For small work, a few lines are enough.

What follows is my interpretation of the course, plus a few things I added.

## Stage 0: Understand the problem

A spec can only be as clear as my understanding of the problem, and the agent fills every gap with a guess. So I think the problem through on my own first and write down how I see it, in my own words. Once the first draft exists, I improve it with the agent.

Before I involve the agent, I write down, on paper or in a note:

- The problem, who has it and why it matters now.
- The outcome I want, and how I would know I have it.
- What I must not break: what exists today and has to keep working, such as a running service, existing data or agreed wording.
- What is out of scope: work I am not asking for, even if it looks useful.
- What I know and what I do not know yet.

Stage 0 comes before the constitution (the standing agreement with the agent, stage 1). The ambiguity check in stage 2, where the agent lists what my written problem leaves open, then sharpens it.

Two cautions:

- The aim is a clear problem, not a finished solution. Keep it to about a page. Heavy up-front design is the waterfall risk that critics warn about, and some clarity only comes from trying. When more clarity stops changing what I would do, I stop.
- That thinking alone first beats thinking with the agent is my opinion. I think it stops me anchoring on the agent's framing.

To improve the first draft with the agent, I use prompts that make it question me instead of proposing solutions: an interview, one question at a time, until the problem is clear.

## Stage 1: Define the constitution

Once I have a clear problem to solve, the next step is a job contract with the agent for the work I want done. It can be called a constitution, a work agreement or a spec. The agent drafts it and I review it, because I cannot rely on the agent to get everything right.

The constitution is the top-level spec: the intent and how the agent works on it, kept as files and read at the start of every session, because the agent remembers nothing from earlier sessions. The course keeps it as a spec directory with three files (mission, tech stack, roadmap). I cover it in four concepts. They can be merged into one note, grouped into a few notes, or kept as one note per concept:

1. **Intent.** The task, what I must not break, what is out of scope, what needs my approval and what the agent must never touch.
2. **Process and tools.** The tools and technology the agent may use, the process it follows, behaviour instructions, and how it reports and records evidence.
3. **Validation.** The definition of done and the criteria for judging the output, with the tools or scripts that check them. It names the end state, how to prove it and what must remain unchanged.
4. **Plan.** The overall order of work, split into phases the agent proposes from the intent and scope. Each phase ends in something I can verify and review in one sitting, and has a checkpoint.

Examples of the boundaries in Intent:

- **Installation:** no changes outside the install directory, ask before anything irreversible, report every command.
- **Code change:** touch only the files in scope, existing tests must still pass, ask before adding a dependency.
- **Data cleanup or migration:** work on a copy, show a dry run before any change, never delete.

How I keep these notes:

- **Drafted once, refined after each phase.** After each review I add what I learned, so the next piece starts from a better agreement.
- **Short.** However they are split, each note must be short enough for the agent to take in at the start of a session and for me to review in one sitting.

## Stage 2: Define phases and tasks

Stage 1 is drafted once and refined after each phase. Stage 2 repeats for each phase of the plan. I specify a phase just in time, after the previous phase has passed its checkpoint, because what I learn in one phase changes what the next one needs. Each phase gets its own folder with a phase spec and a task list, short enough for the agent to take in and for me to review in one sitting:

```
Project/
  Intent.md, Process-and-Tools.md, Validation.md, Plan.md
  Phase-1/
    Phase-Spec.md
    Tasks.md
  Phase-2/
    ...
```

The loop for each phase:

1. **Draft the phase spec.** The agent drafts it from the plan: what this phase delivers and why, how I will know it is done, what is out of scope and the approach. Keep it about behaviour. The approach is the strategy (order of work, main choices), not implementation detail, because that goes out of date quickly.
2. **Ambiguity check.** Before I approve, the agent lists what the spec leaves open and I answer, because the agent guesses when the brief is vague.
3. **I approve the criteria.** I review the done criteria, the verification method and the out-of-scope list line by line, because they decide whether the output can be trusted. Every criterion has a check I can run (a test, or a command with its expected output), or a named review step where no automated check is possible.
4. **Draft the tasks.** Ordered units of work, each small enough to verify on its own, with a precondition, a definition of done, the check and a place for evidence. Each phase criterion maps to at least one task. I review the list once.
5. **Execute task by task.** After each task the agent runs the check and records the evidence (date, command or output) and the status next to the task. Only a passed check marks a task done.
6. **Stop on a failed check or a wrong spec.** The agent records the failure, stops and proposes the spec change. I approve it before work continues, so the spec never drifts silently.
7. **Review the phase.** The checks and a fresh-context reviewer (a separate agent session that sees only the spec and the result) test the result against the phase spec. I review the overall result.
8. **Checkpoint.** My sign-off before the next phase. Always one after the first task of the first phase and at the end of every phase. I loosen the in-phase ones as the pattern proves itself.
9. **Replan and refine.** Update the plan, the scope of the next phase and the constitution with what the phase showed.
10. **Close the phase.** Once the work is accepted, the work is the source of truth and the phase and task specs become a work log. I keep the checks with the work, because they keep proving it. I keep a short decision record: what was out of scope, which approaches were rejected and which spec changes I approved. I archive the rest outside the agent's default reading path and mark it as history, so a later session does not read it as current.

## Validation at every level

Each level of the spec has its own check, written where that level is defined. Lower levels prove the pieces, higher levels prove the whole, and the checks must not contradict each other.

- **Constitution level.** The check proves the job is done: the end state holds and what must remain unchanged still does. The agent runs it at the end of the job, with a fresh-context reviewer.
- **Phase level.** The check proves the delivered behaviour matches the phase spec, like an acceptance test. The agent runs it at the end of the phase, with a fresh-context reviewer.
- **Task level.** The check proves one piece works, like a unit test. The agent runs it right after the task and records the evidence next to the task.

Rules for all levels:

- **Written before the work, approved by me.** The criteria and the check for a level are fixed before that level starts, and I approve them. This is where my review goes.
- **Cover upwards.** Every phase criterion is covered by at least one task check, or has its own check at the end of the phase. Without this mapping, all tasks can pass while a criterion goes untested.
- **Evidence is date, command and output,** recorded next to what it proves. A check without evidence counts as not run. Evidence alone does not prove it ran, because the agent writes it, so the checks that matter are rerun by me, a reviewer or CI.

## Beyond coding agents

My hypothesis is that the method works for any task where I can state the end state and check it. The layers should carry over unchanged. Only the check differs:

- **Deployment.** Done: the service runs, answers on the target machine and survives the failures you planned for. Check: a health-check command with expected output, then the failure scenarios.
- **Troubleshooting.** Done: the cause is shown and the fix removes the symptom. Check: reproduce before the fix, fail to reproduce after.
- **Product documentation.** Done: a new person completes the task using only the page. Check: follow it on a clean environment, then a link and terminology check.
- **Research brief.** Done: every claim carries a source. Check: a script or reviewer confirms each claim has a link.
- **Migration or bulk change.** Done: nothing lost, nothing broken. Check: counts before and after, a link check and a dry run.
- **Proposal or report.** Done: it answers the client's question within the agreed scope. Check: a checklist against the brief and a fresh-context read.

I have started applying this outside code. The work was a deployment of a customer-experience platform on a Kubernetes cluster spread across two sites. The aim was not only to install it once. It was to fix the deployment process: improve the automated deployment script, then test end to end that the platform stays available when parts of it fail.

So the definition of done was a check, not a finished install: after deployment, the high-availability scenarios are tested end to end. I have completed that testing for the two-site deployment.

The agent cannot claim the deployment works without passing those checks, and a new session can resume from the last verified step.

## Does it still hold?

The course teaches spec-first: the spec is written before the work and guides it, and the constitution outlives each task and governs all the work that follows. It does not ask you to adopt a framework; it only refers to Spec Kit and OpenSpec as references.

The course dates from the time of Sonnet 4.6, and models have improved a lot since. What a spec solves has not changed: the agent cannot know my intent, remembers nothing between sessions and should not be trusted unchecked. Better models do not remove those problems, so the essence of the course still holds. What probably loosens is the scaffolding, such as task size and how often I stop for a checkpoint.

## Sources

- [Spec-Driven Development with Coding Agents](https://www.deeplearning.ai/courses/spec-driven-development-with-coding-agents), DeepLearning.AI with JetBrains, Paul Everitt
- [GitHub Spec Kit](https://github.com/github/spec-kit)
- [Anthropic, best practices for Claude Code](https://code.claude.com/docs/en/best-practices), on giving the agent a way to verify its work and show evidence
