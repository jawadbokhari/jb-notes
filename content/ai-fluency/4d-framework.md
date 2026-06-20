---
Course:
  - "[[AI Fluency]]"
---


Delegate to AI for: 
- Automation: The AI completes specific tasks based on your instructions.
- Augmentation: You and AI collaborate as creative thinking and task execution partners.
- Agency: You configure AI to work independently on your behalf, establishing its knowledge and behavior patterns.

## The Description-Discernment loop

This is about effective conversation and not just a command. 
Build **shared understanding** with AI instead of copying prompts from others and build
- shared vocabulary and references 
- well-defined goals
- values, processes, and methods


As you iterate through Description-Discernment cycles, you and the AI co-create valuable knowledge:

- Guidelines that emerged from trial and error
- Patterns that worked well
- Insights discovered through the conversation
- Refined understanding of what "good" looks like
- Lessons about what to avoid

Preserve this shared understanding out of the messy conversation context. 

### 1. **Explicit Extraction Sessions**

Periodically pause and ask questions like:

- _"Based on our iterations, what guidelines have we discovered?"_
- _"Summarize the key lessons from this refinement process"_
- _"What should I remember for next time I do this task?"_

Then save that distilled knowledge externally (my preference is markdown files stored in a git repository)

### 2. **Create "Learned Patterns" Documents**

After a successful loop, capture:
Task: __What we were working on__
What worked: __Successful approaches__
What didn't: __Failed attempts and why__
Key guidelines discovered: __Rules we developed__
Success criteria: __How we knew it was good__



### 3. **Update Project Instructions/Skills**

Take the emergent guidelines and:
- Add them to **Project custom instructions**
- Build them into **Skills** for reuse

### 4. **Use Memory Edits**

For personal patterns you discover:

- _"Remember that when I ask for X type of content, I prefer Y approach based on our iterations today"_


### **The Feedback Pattern**
What makes it a "loop" is how discernment _informs_ the next description:

- You notice a gap → You add context
- You see misalignment → You clarify intent
- You spot a good element → You ask to amplify it
- You detect wrong reasoning → You explain your logic

## Building Shared Understanding
The "shared cognitive environment" emerges through specific **interaction patterns**:

### **Pattern 1: Progressive Refinement**

```
Round 1: Vague description → Generic output → "Too broad"
Round 2: Add constraints → Better output → "Right direction, but..."
Round 3: Provide example → Aligned output → "Perfect"
```

Each iteration narrows the gap between intent and execution.

### **Pattern 2: Constraint Discovery**

You don't always know all your requirements upfront:

```
You: "Create a summary"
AI: [produces summary]
You: "Actually, I need it to avoid jargon" ← constraint discovered through discernment
AI: [revised version]
You: "And keep it under 3 sentences" ← another constraint emerges
```

### **Pattern 3: Collaborative Problem-Solving**

```
You: Describe problem
AI: Proposes solution A
You: "A won't work because X" ← discernment reveals hidden constraint
AI: Proposes solution B accounting for X
You: "Better, but what about Y?" ← new consideration surfaces
AI: Integrated solution addressing X and Y
```

### **Pattern 4: Example-Driven Alignment**

```
You: Initial description
AI: Output 1
You: "More like this [example], less like that" ← showing, not just telling
AI: Output 2 (closer)
You: "Yes! Now apply that same principle to Z"
```

### **Pattern 5: Meta-Reflection**

```
You: "Why did you choose approach X?"
AI: Explains reasoning
You: "Ah, you're optimizing for Y, but I actually need Z" ← reveals misaligned assumptions
AI: Reframes with correct optimization target
```

### **Pattern 6: Assumption Surfacing**

```
You: Describe task
AI: Produces output
You: "What assumptions did you make?"
AI: Lists assumptions
You: "Assumption X is wrong — here's the actual context" ← catches misalignment before it compounds
```

### **Pattern 7: Parallel Branching**

```
You: "Give me 3 different approaches to this"
AI: Options A, B, C
You: "I like the structure of A but the tone of C" ← triangulates what "good" looks like faster than sequential iteration
```

### **Pattern 8: Devil's Advocate**

Ask the *same* AI to argue against its own output — within the conversation.

```
You: "Now argue against what you just said"
AI: Critiques its own output
You: "That third objection is valid — revise with that in mind" ← surfaces blind spots in AI's own reasoning
```

### **Pattern 9: Vocabulary Alignment**

```
You: "When I say 'simple', I mean accessible to a non-technical reader, not brief"
AI: Acknowledges and applies your definition throughout ← prevents semantic drift across a long conversation
```

### **Pattern 10: Checkpoint Calibration**

```
You: "Before you write the full thing — summarize your plan in 3 bullets"
AI: Outlines approach
You: "Change bullet 2, then proceed" ← cheap to correct a plan vs. a finished output
```

### **Pattern 11: Adversarial Agent**

Different from Devil's Advocate — this is an *architectural* pattern where a **separate AI instance** is configured specifically to red-team or stress-test the output of another AI.

```
Agent A (Generator): Produces a plan or output
Agent B (Adversary): Independently configured to find flaws, edge cases, or risks
You: Review both, decide what holds up ← two AI perspectives surface more blind spots than one
```

Used in agentic workflows where the stakes are high enough to warrant a dedicated critic. The adversary agent has no loyalty to Agent A's output — it's structurally incentivized to break it.


- Automation - get a task completed, e.g., plan a trip, translate a message, or solve a math problem (when you are clear what you want to achieve)
- Augmentation - creative thinking partner to explore (when you are not clear about your objectives)
- Agency - when human configure AI to work independently on their behalf including interacting with other human or AI. you get AI do a relatively complex multi-step work, for example, categorize high priority emails and respond to the most important ones.



## Descriptions 
The 3Ps for your Description competency of AI Fluency.  
### Product Description
- Define "What" do you want to achieve? 
- who is the audience? 
- what is the problem context? 
- How should AI respond? the style, tone, etc. 
- What are the constraints? 
Develop shared understanding iteratively on refining the "what" and "what success looks like"

### Process Description
How should AI achieve this goal - the process?
- Maybe share how I would have done it? or how I recently solved a similar problem? 
- some specific algorithm, technique you want to use
- some specific data you want to highlight 
- preferred order 

What steps to follow, which tools to use, etc. Agree on a set of instructions to follow. 

### Performance Description 
Define the behavioral aspect of AI interaction. Specify, how do you want AI to behave in this "intellectual partnership"
- should it just answer without mentioning the reason
- should it be more critical
- should it answer or just ask you question to drive you towards your goal
- should the answer be concise, detailed, or what

### Discernment
- Understand how to evaluate AI outputs and processes thoughtfully
- Develop critical thinking skills for your AI interactions
- Identify and address quality concerns in your AI interactions

1. Product Discernment - quality of the output
2. Process Discernment - quality of reasoning
	- did it think through the problem logically?
	- did it approach the problem correctly? 
	- did it choose the right method? 
	- did it sequence the work well?
3. **Performance Discernment** - how it communicates, quality of interaction, behavior
	- Was it **clear** in how it explained itself?
	- Did it **ask good clarifying questions**?
	- Did it **build on your feedback**, or ignore it?
	- Was it **responsive to your direction** during the conversation?
## Diligence
This competency focus on taking responsibility for AI collaboration. 
ethical and safety aspects.


- Creation Diligence: Being thoughtful about which AI systems you choose and how you work with them
- Transparency Diligence: Being open about AI's role in your work
	- who needs to know and how much that AI was used in this work? 
- Deployment Diligence: Taking ownership for AI-assisted outputs you share with others



## Applying 4Ds

- **Delegation:** What aspects of this project would you handle yourself vs. collaborate on with AI?
- **Description:** How would you communicate your vision for the campaign's tone, purpose, and success criteria to the AI?
- **Discernment:** What criteria would help you evaluate whether the AI-drafted emails meet your needs?
- **Diligence:** What considerations around transparency and responsibility would be important?

1. Choose a project: Think of something that you want to do in collaboration with AI. 
2. Partner with AI to define your project vision and goals
	1. What is the overall vision for the task? What does a good result look like?
	2. what success looks like? 
	3. What would make it valuable?
	4. What are the different chunks of work needed to get there?
	5. Which of these chunks of work require human expertise, creativity, or judgment?
3. Identify major tasks together
4. For each task, one at a time: **have a genuine conversation with AI** 
	1. What skills, knowledge, or AI capabilities are needed? 
	2. Which parts would benefit from unique human strengths? 
	3. Which parts could leverage AI capabilities well? 
	4. Where might collaboration have the most impact? 