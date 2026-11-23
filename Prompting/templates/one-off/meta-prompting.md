---
title: "Templates: Meta-prompting"
---

Prompts that work on a prompt instead of the task. Technique and when to use it: [[../../techniques/advanced#6. Meta-prompting|Advanced Techniques, meta-prompting]]. Each template asks for something you can check (a list, a rewrite, test cases), not for the model's reasoning.

| Use case                                       | Template                                      |
| ---------------------------------------------- | --------------------------------------------- |
| Ambiguous or high-stakes task, before starting | 1. Ask what's missing                         |
| You know the goal, not the prompt              | 2. Draft a prompt from a goal                 |
| Existing prompt gives mediocre results         | 3. Improve a prompt                           |
| Long instruction file or system prompt         | 4. Conflict check                             |
| One specific bad output                        | 5. Diagnose a failure                         |
| Prompt you will reuse                          | 6. Generate test cases                        |
| A chat that went well                          | 7. Turn a conversation into a reusable prompt |
| Moving a prompt to another model or tool       | 8. Port a prompt                              |

## 1. Ask what's missing

```
Before you start: [task in one or two sentences].

List the information you need from me to do this well, most important first, at most [5] questions. For each, say what you would assume if I don't answer. Do not start the task yet.
```

## 2. Draft a prompt from a goal

```
Write a prompt I can give to [model or tool] to [goal].

Context: [who the output is for, where it will be used]
Inputs it will receive: [what I will paste or attach]
Good output looks like: [format, length, tone, one example if I have it]
Must not: [known failure modes]

Return only the prompt, under [N] words. Then list the assumptions you made that I should check.
```

## 3. Improve a prompt

```
Here is a prompt and an output it produced that I'm not happy with.

Prompt:
"""[prompt]"""

Output:
"""[output]"""

What I wanted instead: [one or two sentences]

1. List the three changes to the prompt most likely to close that gap.
2. Rewrite the prompt with those changes.
3. Critique your rewrite: what did it add that isn't needed?
4. Give the final version, no longer than [the original / N words].
```

## 4. Conflict check

```
Review these instructions:
"""[instruction file or system prompt]"""

List:
- Contradictions: pairs of rules that pull in different directions (for example brevity vs. completeness, act autonomously vs. ask first). Quote both.
- Redundancies: rules that say the same thing, or that the model does anyway.
- Vague rules: ones two readers would apply differently.

For each, propose the smallest edit that fixes it. Do not rewrite the whole file.
```

## 5. Diagnose a failure

```
This prompt produced the output below. The problem: [what went wrong, concretely].

Prompt: """[prompt]"""
Output: """[output]"""

Point to the part of the prompt (quote it) that most likely led to this, or the missing instruction. Propose one minimal edit. Then give two other inputs where the edited prompt could still fail.
```

> The model's account of why it failed is a hypothesis, not a fact. Confirm the fix by re-running the prompt (template 6 helps).

## 6. Generate test cases

```
I'll reuse this prompt:
"""[prompt]"""

Write [8] test inputs: [4] typical, [2] edge cases, [2] that tempt a known failure ([failure]). For each, state in one line what a correct output must contain or avoid, as yes-or-no checks.
```

Run the prompt on each input, score against the checks, and keep the set for when the prompt or model changes.

## 7. Turn a conversation into a reusable prompt

```
This conversation produced the result I wanted. Write a single prompt that would get the same result in one turn next time, for a new [input type].

Include the context and corrections I gave along the way. Leave out anything specific to this instance, marking it as [placeholder]. Under [N] words.
```

## 8. Port a prompt

```
This prompt works well on [source model or tool]:
"""[prompt]"""

Adapt it for [target model or tool]. Account for: [differences I know, for example no file access, smaller context, different tool names]. List each change and why, then give the adapted prompt. Change nothing that doesn't need to change.
```
