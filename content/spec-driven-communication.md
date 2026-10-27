---
title: Spec-Driven Communication
tags:
  - ai
  - spec-driven-development
  - coding-agents
---

Paul Everitt's [Spec-driven development](https://www.deeplearning.ai/courses/spec-driven-development-with-coding-agents) course is an excellent beginner course on the fundamentals of spec-driven communication (mainly for coding agents), but for me it unlocked how we build shared understanding with AI so that we can efficiently delegate longer tasks to it with higher confidence.

In a nutshell, spec-driven communication is agreeing with an agent in writing, in layers from strategic to tactical: a spec for the intent, then for each phase, then for each task. Every spec states what I want, what is out of scope and how I will know it is done. Standing rules apply to all of it. I approve the criteria, and the agent's work is checked against them by a test or a separate reviewer. After each piece of work I update the specs and rules. For small work, a few lines are enough.


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

> To improve the first draft with the agent, I use skills that make it question me instead of proposing: `grill-me` and the BMad brainstorming skills (`bmad-brainstorming`, `bmad-cis-agent-brainstorming-coach`).

## Stage 1: Define the constitution

Once I have a clear problem to solve, the next step is defining a job-contract with the agent to delegate the work I want done. It can be called a constitution, a work agreement or a spec. It covers the areas I want agreed at the contract level. The agent drafts it and I review it, because I cannot rely on the agent to get everything right.

The constitution is the top-level **spec**: the intent and how the agent works on it, kept as files and read at the start of every session, because the agent remembers nothing from earlier sessions. The course keeps it as a spec directory with three files (mission, tech stack, roadmap). I cover it in four concepts. They can be merged into a single note, grouped into a set of notes, or kept as one note per concept, with these file names:

| # | Note | Covers |
| --- | ------ | -------- |
| 1 | Intent.md | The task, what I must not break, what is out of scope, what needs my approval and what the agent must never touch. The definition of done lives in Validation.md. |
| 2 | Process-and-Tools.md | The tools and technology the agent may use, the process it follows, behaviour instructions, and how it reports and records evidence. |
| 3 | Validation.md | The definition of done and the criteria for judging the output, with the tools or scripts that check them. It names the end state, how to prove it and what must remain unchanged. |
| 4 | Plan.md | The overall order of work, split into phases the agent proposes from the intent and scope. Each phase ends in something I can verify and review in one sitting, and has a checkpoint. Stage 2 specifies each phase and its tasks. |

Examples of the boundaries in Intent:
- **Installation:** no changes outside the install directory, ask before anything irreversible, report every command.
- **Code change:** touch only the files in scope, existing tests must still pass, ask before adding a dependency.
- **Data cleanup or migration:** work on a copy, show a dry run before any change, never delete.

How I keep the notes:
- **Drafted once, refined after each phase.** After each review I add what I learned, so the next piece starts from a better agreement.
- **Size.** However they are split, each note must be short enough for the agent to take in at the start of a session and for me to review in one sitting.

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
1. **Draft the phase spec** (`Phase-Spec.md`). The agent drafts it from `Plan.md`: what this phase delivers and why, how I will know it is done, what is out of scope and the approach. Keep it about behaviour. The approach is the strategy (order of work, main choices), not implementation detail, because that goes out of date quickly.
2. **Ambiguity check.** Before I approve, the agent lists what the spec leaves open and I answer, because the agent guesses when the brief is vague.
3. **I approve the criteria.** I review the done criteria, the verification method and the out-of-scope list line by line, because they decide whether the output can be trusted. Every criterion has a check I can run (a test, or a command with its expected output), or a named review step where no automated check is possible. Phase checks refine `Validation.md` and do not replace it (see "Validation at every level").
4. **Draft the tasks** (`Tasks.md`). Ordered units of work, each small enough to verify on its own, with a precondition, a definition of done, the check and a place for evidence. Each phase criterion maps to at least one task. I review the list once.
5. **Execute task by task.** After each task the agent runs the check and records the evidence (date, command or output) and the status next to the task. Only a passed check marks a task done.
6. **Stop on a failed check or a wrong spec.** The agent records the failure, stops and proposes the spec change. I approve it before work continues, so the spec never drifts silently.
7. **Review the phase.** The checks and a fresh-context reviewer (a separate agent session that sees only the spec and the result) test the result against the phase spec. I review the overall result.
8. **Checkpoint:** my sign-off before the next phase. Always one after the first task of the first phase and at the end of every phase. Loosen the in-phase ones as the pattern proves itself.
9. **Replan and refine.** Update `Plan.md`, the scope of the next phase and the constitution with what the phase showed.
10. **Close the phase.** Once the work is accepted, the work is the source of truth and the phase and task specs become a work log. I keep the checks with the work, because they keep proving it. I keep a short decision record: what was out of scope, which approaches were rejected and which spec changes I approved. I archive the rest outside the agent's default reading path and mark it as history, so a later session does not read it as current.

How each level is validated is set out in the next section.

## Validation at every level

Each level of the spec has its own check, written where that level is defined. Lower levels prove the pieces, higher levels prove the whole, and the checks must not contradict each other.

| Level | Specified in | The check proves | Run by | Evidence recorded in |
|---|---|---|---|---|
| Constitution | `Validation.md` | The job is done: the end state holds and what must remain unchanged still does | Agent at the end of the job, with a fresh-context reviewer | `Validation.md` or the job log |
| Phase | `Phase-Spec.md` (done criteria) | The delivered behaviour matches the phase spec, like an acceptance test | Agent at the end of the phase, with a fresh-context reviewer | `Phase-Spec.md` |
| Task | `Tasks.md` (check per task) | One piece works, like a unit test | Agent right after the task | `Tasks.md`, next to the task |

Rules for all levels:
- **Written before the work, approved by me.** The criteria and the check for a level are fixed before that level starts, and I approve them. This is where my review goes.
- **Cover upwards.** Every phase criterion is covered by at least one task check, or has its own check at the end of the phase. Without this mapping, all tasks can pass while a criterion goes untested.
- **Evidence is date, command and output,** recorded next to what it proves. A check without evidence counts as not run. Evidence alone does not prove it ran, because the agent writes it, so the checks that matter are rerun by me, a reviewer or CI.

## Beyond coding agents

My hypothesis is that the method works for any task where I can state the end state and check it. The layers should carry over unchanged. Only the check differs.

| Work                     | Done looks like                                       | The check                                                    |
| ------------------------ | ----------------------------------------------------- | ------------------------------------------------------------ |
| Installation             | The service runs and answers on the target machine    | A health-check command with expected output                  |
| Troubleshooting          | The cause is shown, the fix removes the symptom       | Reproduce before the fix, fail to reproduce after            |
| Product documentation    | A new person completes the task using only the page   | Follow it on a clean environment; link and terminology check |
| Research brief           | Every claim carries a source                          | A script or reviewer checks each claim has a link            |
| Migration or bulk change | Nothing lost, nothing broken                          | Counts before and after; link check; dry run                 |
| Proposal or report       | Answers the client's question within the agreed scope | A checklist against the brief; fresh-context read            |

Untested example:

- **Installation.** Constitution: no changes outside the install directory, ask before anything irreversible, report every command. Phase spec: install X version N on host Y; done when the health endpoint returns OK and survives a reboot; out of scope: data migration and tuning. Tasks: each has a precondition ("port 8080 is free"), a command and its output as evidence, with a checkpoint before the first change. The agent cannot claim success without the health check, and a new session resumes from the last verified task.

## Conclusions

The course teaches spec-first: the spec is written before the work and guides it, and the constitution outlives each task and governs all the work that follows. It does not ask me to adopt a framework; it only refers to Spec Kit and OpenSpec as references.

**My interpretations:**
- Build the shared understanding step by step, as written files in the project: first the constitution, then each phase, then each task.
- Each task has preconditions, a definition of done and evidence, so the agent shows what it did.
- I define the validation method, the agent drafts and I review.
- A constitution split into four notes, with validation specified at every level.
- The agreement improves as the work goes on. After each phase I replan and refine the constitution, so the next piece starts from a better agreement.

**Does it still hold?** The course dates from the time of Sonnet 4.6, and models have improved a lot since. What a spec solves has not changed: the agent cannot know my intent, remembers nothing between sessions and should not be trusted unchecked. Better models do not remove those problems, so the essence of the course still holds. What probably loosens is the scaffolding, such as task size and how often I stop for a checkpoint.

## Sources

- Spec-Driven Development with Coding Agents (DeepLearning.AI with JetBrains, Paul Everitt): https://www.deeplearning.ai/courses/spec-driven-development-with-coding-agents
- GitHub Spec Kit: https://github.com/github/spec-kit
- Anthropic, on giving the agent a way to verify its work and show evidence: https://code.claude.com/docs/en/best-practices
