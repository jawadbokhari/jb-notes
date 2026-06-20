---
Course:
  - "[[AI Fluency]]"
---
Description is about effective conversation, not just commands. The goal is to build a **shared understanding** with AI — a productive collaborative environment where both you and AI operate from the same vocabulary, goals, and values.

Instead of copying prompts from others, invest in building:
- shared vocabulary and references
- well-defined goals
- values, processes, and methods

## The 3Ps

### Product Description
Define **what** you want to achieve:
- Who is the audience?
- What is the problem context?
- How should AI respond — style, tone, format?
- What are the constraints?

Develop shared understanding iteratively on refining the "what" and "what success looks like."

### Process Description
Define **how** AI should achieve the goal:
- How would you have done this yourself?
- Is there a specific algorithm, technique, or data to use?
- What's the preferred order of steps?
- Which tools should be used?

Agree on a set of instructions to follow — not just the output, but the path to get there.

### Performance Description
Define the **behavioral** aspect of the interaction. How should AI behave as an intellectual partner?
- Should it just answer, or explain its reasoning?
- Should it be more critical or more supportive?
- Should it ask you questions, or drive toward a direct answer?
- Should the response be concise, detailed, or something else?

---

## The Description–Discernment Loop

Description doesn't happen once. Every exchange with AI is a loop: you describe, you evaluate what comes back ([[Discernment]]), and your evaluation informs how you describe better next time. The goal is to tighten this loop — narrowing the gap between what you meant and what AI produced.

What makes it a loop is how discernment _informs_ the next description:

- You notice a gap → You add context
- You see misalignment → You clarify intent
- You spot a good element → You ask to amplify it
- You detect wrong reasoning → You explain your logic

### Interaction Patterns

**Pattern 1: Progressive Refinement**
```
Round 1: Vague description → Generic output → "Too broad"
Round 2: Add constraints → Better output → "Right direction, but..."
Round 3: Provide example → Aligned output → "Perfect"
```

**Pattern 2: Constraint Discovery**

You don't always know all your requirements upfront:
```
You: "Create a summary"
AI: [produces summary]
You: "Actually, I need it to avoid jargon" ← constraint discovered through discernment
AI: [revised version]
You: "And keep it under 3 sentences" ← another constraint emerges
```

**Pattern 3: Collaborative Problem-Solving**
```
You: Describe problem
AI: Proposes solution A
You: "A won't work because X" ← discernment reveals hidden constraint
AI: Proposes solution B accounting for X
You: "Better, but what about Y?" ← new consideration surfaces
AI: Integrated solution addressing X and Y
```

**Pattern 4: Example-Driven Alignment**
```
You: Initial description
AI: Output 1
You: "More like this [example], less like that" ← showing, not just telling
AI: Output 2 (closer)
You: "Yes! Now apply that same principle to Z"
```

**Pattern 5: Meta-Reflection**
```
You: "Why did you choose approach X?"
AI: Explains reasoning
You: "Ah, you're optimizing for Y, but I actually need Z" ← reveals misaligned assumptions
AI: Reframes with correct optimization target
```

**Pattern 6: Assumption Surfacing**
```
You: Describe task
AI: Produces output
You: "What assumptions did you make?"
AI: Lists assumptions
You: "Assumption X is wrong — here's the actual context" ← catches misalignment before it compounds
```

**Pattern 7: Parallel Branching**
```
You: "Give me 3 different approaches to this"
AI: Options A, B, C
You: "I like the structure of A but the tone of C" ← triangulates what "good" looks like faster than sequential iteration
```

**Pattern 8: Devil's Advocate**

Ask the *same* AI to argue against its own output — within the conversation.
```
You: "Now argue against what you just said"
AI: Critiques its own output
You: "That third objection is valid — revise with that in mind" ← surfaces blind spots in AI's own reasoning
```

**Pattern 9: Vocabulary Alignment**
```
You: "When I say 'simple', I mean accessible to a non-technical reader, not brief"
AI: Acknowledges and applies your definition throughout ← prevents semantic drift across a long conversation
```

**Pattern 10: Checkpoint Calibration**
```
You: "Before you write the full thing — summarize your plan in 3 bullets"
AI: Outlines approach
You: "Change bullet 2, then proceed" ← cheap to correct a plan vs. a finished output
```

**Pattern 11: Adversarial Agent**

Different from Devil's Advocate — this is an *architectural* pattern where a **separate AI instance** is configured specifically to red-team or stress-test the output of another AI.
```
Agent A (Generator): Produces a plan or output
Agent B (Adversary): Independently configured to find flaws, edge cases, or risks
You: Review both, decide what holds up ← two AI perspectives surface more blind spots than one
```

Used in agentic workflows where the stakes are high enough to warrant a dedicated critic. The adversary agent has no loyalty to Agent A's output — it's structurally incentivized to break it.

---

## Preserving Shared Understanding

As you iterate through Description–Discernment cycles, you and the AI co-create valuable knowledge:
- Guidelines that emerged from trial and error
- Patterns that worked well
- Insights discovered through the conversation
- Refined understanding of what "good" looks like
- Lessons about what to avoid

Preserve this out of the messy conversation context:

1. **Explicit Extraction Sessions** — Periodically pause and ask: _"Based on our iterations, what guidelines have we discovered?"_ Then save that distilled knowledge externally (markdown files in a git repository work well).

2. **Create "Learned Patterns" Documents** — After a successful loop, capture:
   - Task: What we were working on
   - What worked: Successful approaches
   - What didn't: Failed attempts and why
   - Key guidelines discovered: Rules we developed
   - Success criteria: How we knew it was good

3. **Update Project Instructions/Skills** — Add emergent guidelines to project custom instructions or build them into reusable skills.

4. **Use Memory Edits** — For personal patterns: _"Remember that when I ask for X type of content, I prefer Y approach based on our iterations today."_

---

*Prev: [[Delegation]] · Next: [[Discernment]]*
