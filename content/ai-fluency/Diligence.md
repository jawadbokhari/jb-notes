---
Course:
  - "[[AI Fluency]]"
---
> [!info] AI disclosure
> Drafted with Claude's help and reviewed by me. Based on the [AI Fluency Framework course](https://academy.claude.com/courses/ai-fluency-framework-foundations).

Diligence is about taking responsibility for your AI collaboration. It's the ethical and accountability dimension of AI Fluency: being thoughtful about which AI systems you use, being honest about their role in your work, and owning the outcomes you share with others.

## The 3 Dimensions of Diligence

### Creation Diligence
Be thoughtful about **which AI systems you choose** and how you work with them:
- Is this the right tool for this task?
- What are the known limitations of this system?
- Are you using it in a way that's appropriate given the stakes?

### Transparency Diligence
Be open about **AI's role in your work**:
- Who needs to know that AI was used here?
- How much disclosure is appropriate given the context?
- Are you representing AI-assisted work accurately to your audience?

### Deployment Diligence
**Own the final output** you share with others:
- Have you verified the output is accurate?
- Are you comfortable standing behind this work?
- What happens if the AI got something wrong?

## Diligence in everyday communication

Diligence is mostly about ordinary messages, not published work. Here is how it looks in practice.

### Example: the message that is too long

In an agentic session, the agent often drafts an email or chat message for a colleague. The draft is often too long and hard to follow, and this happens so often that it becomes a habit. The sender has the whole session in mind, so the draft reads as clear. The reader has none of that context, and pays for the length with their attention.

A label saying "AI-generated" does not fix this: it tells the reader what they are holding, not whether it is worth reading. Each of the four Ds has a part in the fix:

- **Delegation (before).** Decide whether the agent should draft this at all. A two-line answer is often faster to write yourself than to cut down.
- **Description (before).** Tell the agent who the reader is, what you want from them and how long the message may be. For example: "Five lines, the ask first, no background the reader already has."
- **Discernment (during).** Read the draft as the recipient would, as if you had never seen the session. Can they tell what you want in the first two lines? Is anything there only because the agent happened to have it?
- **Deployment Diligence (at send).** Sending is the moment you own the message. The test: can the reader act on it in about 30 seconds? If not, shorten it yourself before it goes.
- **Transparency Diligence (with the message).** If the message is still long, say at the top that AI drafted it, so the reader can skim it or hand it to their own assistant. This is the fallback, not the fix.

### Other places it applies

- **Emails and chat messages.** AI can draft them, but I read and edit every one before I send it, and cut it to what the reader needs. If it is still long, a short note at the top lets the reader skim it or hand it to their own assistant.
- **Meeting notes.** Notes generated from a meeting recording are labelled as AI-generated, because they can miss a decision or put words in someone's mouth. I fix them before anyone acts on them.
- **Code commits.** My [agent git guidelines](https://github.com/jawadbokhari/agent-git-guidelines) make this a written rule. Every commit an agent drafted or materially changed carries an `Assisted-by:` line naming the agent, so reviewers know to check it as AI-assisted work (P1). Only a human adds `Signed-off-by:`, because that line certifies that a person reviewed the change (Deployment Diligence). A label is not proof of checking (P5), so disclosure does not replace review.
- **Articles and notes.** This note has a disclosure line at the top, so readers know AI helped and that I reviewed it.

### A simple rule

Shorten first, disclose second. Cut the message until the reader can act on it in about 30 seconds. Then put the disclosure at the top, in one line: what AI did (drafted, summarised, translated) and what you did (reviewed, corrected, approved). That way the reader does not have to guess.

---

> [!note] Diligence and the other Ds
> In Anthropic's diagram, Diligence is linked to Delegation, Description and Discernment. The course says the other three competencies mainly address working effectively and efficiently, while Diligence addresses the ethical and safety side. When you share AI-generated content, you, not the AI, are responsible for its accuracy and appropriateness (Lesson 10, A closer look at Diligence).

---

*Prev: [[Discernment]] · Next: [[4d-framework|Applying the 4Ds]]*
