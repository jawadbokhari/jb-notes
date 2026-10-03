
> [!tip] The feedback pattern
> Each discernment observation feeds back into your next description:
> - You notice a gap → You add context
> - You see misalignment → You clarify intent
> - You spot a good element → You ask to amplify it
> - You detect wrong reasoning → You explain your logic

---

## The Description–Discernment Loop

Description doesn't happen once. Every exchange with AI is a loop: you describe, you evaluate what comes back ([[Discernment]]), and your evaluation informs how you describe better next time. The goal is to tighten this loop — narrowing the gap between what you meant and what AI produced.

What makes it a loop is how discernment _informs_ the next description:

- You notice a gap → You add context
- You see misalignment → You clarify intent
- You spot a good element → You ask to amplify it
- You detect wrong reasoning → You explain your logic

### Interaction Patterns


**Pattern: Assumption Surfacing**
```
You: Describe task
AI: Produces output
You: "What assumptions did you make?"
AI: Lists assumptions
You: "Assumption X is wrong — here's the actual context" ← catches misalignment before it compounds
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