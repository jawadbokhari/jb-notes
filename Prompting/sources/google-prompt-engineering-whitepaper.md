---
title: "Source: Prompt Engineering Whitepaper (Google, Lee Boonstra)"
---

Condensed extraction of *Prompt Engineering* (Lee Boonstra, Google, September 2024, v4). Focused on Gemini/Vertex AI Studio but the techniques are model-agnostic. Page numbers below refer to the whitepaper's own pagination (footer numbers, not PDF page count).

## LLM output configuration (p.8-11)

**Output length** (p.8): max tokens to generate. Shorter output length doesn't make the model more concise stylistically, it just truncates once the limit is hit. If you need short output, engineer the prompt for brevity too. Especially important for techniques like ReAct, where the model keeps emitting useless tokens past the answer you want.

**Temperature** (p.9): controls randomness of token selection. Lower = more deterministic, higher = more diverse/unexpected. Temperature 0 (greedy decoding) always picks the highest-probability token (ties may still break randomly). As temperature rises toward the max, all tokens trend toward equal likelihood.

**Top-K and top-P** (p.10):
- Top-K: sample from the K most likely tokens. Higher K = more creative/varied, lower K = more restrictive/factual. Top-K of 1 = greedy decoding.
- Top-P (nucleus sampling): sample from the smallest set of tokens whose cumulative probability doesn't exceed P. Range 0 (greedy) to 1 (full vocabulary).
- Best approach: experiment with both (or together) and see what works.

**Putting it together** (p.11): if temperature, top-K and top-P are all set, tokens are filtered by top-K and top-P first, then temperature samples among the survivors. At extreme settings, one control cancels the others out (temperature 0 makes top-K/top-P irrelevant; top-K 1 makes temperature/top-P irrelevant; top-P near 0 makes temperature/top-K irrelevant).

**Recommended starting points** (p.11):

| Goal | Temperature | Top-P | Top-K |
|---|---|---|---|
| Balanced / coherent but creative | 0.2 | 0.95 | 30 |
| Especially creative | 0.9 | 0.99 | 40 |
| Less creative | 0.1 | 0.9 | 20 |
| Single correct answer (e.g. math) | 0 | - | - |

Note: with more freedom (higher temp/top-K/top-P/output length), output can drift less relevant.

## Prompting techniques (p.12-53)

**Zero-shot** (p.13): task description + input only, no examples. Simplest prompt type. Example: classify movie review sentiment with low temperature (no creativity needed).

**One-shot & few-shot** (p.14-16): providing 1 (one-shot) or several (few-shot) examples teaches the model the desired pattern/structure/tone, not just the content. Rule of thumb: 3-5 examples minimum; more for complex tasks, fewer if input-length constrained. Examples must be relevant, diverse, high quality, well written, one bad example confuses the model. Include edge cases if you need robust output.

**System, contextual and role prompting** (p.17-24): three distinct but overlapping techniques.
- **System prompting**: sets overall context/purpose, the "big picture" (translate, classify, output format like JSON, safety/toxicity instructions like "be respectful"). Forces structure and limits hallucination, e.g. requesting JSON output.
- **Contextual prompting**: task-specific background info for the immediate conversation, dynamic and specific to the current ask.
- **Role prompting**: assigns the model a character/identity (e.g. "act as a travel guide"), shapes tone/style/voice. Effective style words listed: Confrontational, Descriptive, Direct, Formal, Humorous, Influential, Informal, Inspirational, Persuasive.
- Purpose distinction: system = fundamental capability, contextual = immediate task info, role = output style/voice.

**Step-back prompting** (p.25-28): first ask the model a general/abstract question related to the task, feed that answer back as context into the specific-task prompt. Activates background knowledge and reduces bias/randomness vs. going straight to the specific ask. Example: instead of "write a shooter-level storyline" directly, first ask "what are 5 fictional key settings for engaging shooter levels", then feed the chosen setting back into the storyline prompt.

**Chain of Thought (CoT)** (p.29-31): ask the model to generate intermediate reasoning steps before the final answer ("Let's think step by step"). Low-effort, high-value, works on off-the-shelf models (no finetuning). Gives interpretability (you can see and debug the reasoning). Improves robustness across model version changes. Downside: more output tokens = more cost/latency. Can combine with one-shot/few-shot for harder tasks. Good for math, code generation, any task you could "talk through."

**Self-consistency** (p.32-35): CoT uses greedy decoding, which caps its reliability. Self-consistency samples the same zero-shot CoT prompt multiple times at high temperature, extracts the answer from each run, and takes the majority vote. Gives a pseudo-probability of correctness but is expensive (many calls per question). Steps: (1) generate diverse reasoning paths at high temperature, (2) extract the answer from each, (3) pick the most common answer.

**Tree of Thoughts (ToT)** (p.36): generalizes CoT, explores multiple reasoning branches simultaneously (a tree, not a single chain) instead of one linear path. Suited to complex tasks needing exploration. Based on Yao et al., "Tree of Thoughts: Deliberate Problem Solving with LLMs."

**ReAct (reason & act)** (p.37-39): combines natural-language reasoning with external tool use (search, code interpreters, APIs) in a thought-action-observation loop: reason -> act -> observe -> update reasoning -> repeat until solved. First step toward agent modeling. Demoed with LangChain + VertexAI + SerpAPI: the model chains 5 searches to answer "how many kids do Metallica band members have," reasoning between each search result.

**Automatic Prompt Engineering (APE)** (p.40-41): use the model to generate prompt variants, score them (e.g. BLEU/ROUGE), keep the best, iterate. Example: generate 10 semantically-equivalent phrasings of a t-shirt order to train a chatbot's intent recognition.

**Code prompting** (p.42-53): four sub-uses, all demoed with gemini-pro, low temperature (0.1), no top-K/top-P limits:
- **Writing code** (p.42-43): e.g. generate a Bash script to rename files. Still requires reading and testing output, the model can't reason and repeats training-data patterns.
- **Explaining code** (p.44-45): paste code, ask for an explanation, useful for reading unfamiliar code in a team.
- **Translating code** (p.46-47): e.g. Bash to Python. Note: in Vertex AI Studio, must click "Markdown" or output loses indentation, breaking Python.
- **Debugging and reviewing code** (p.48-53): paste the traceback and the code, ask the model to debug and suggest improvements. In the example, the model both fixed the reported `NameError` and proactively flagged 4 further issues (extension handling, spaces in folder names, f-string style, missing error handling).

**Multimodal prompting** (p.54): a separate concern from code prompting, combining text with other input formats (image, audio, code) rather than relying on text alone.

## Best Practices (p.54-63)

| Practice | Key point | Page |
|---|---|---|
| Provide examples | Single most important practice; one/few-shot examples teach accuracy, style and tone by demonstration | 54 |
| Design with simplicity | Concise, clear language; if it confuses you it will confuse the model; use action verbs (Act, Analyze, Categorize, Classify, Compare, Create, Describe, Evaluate, Extract, Generate, List, Organize, Rank, Recommend, Rewrite, Summarize, Translate, Write, etc.) | 55-56 |
| Be specific about the output | Concise instructions can be too generic; state length, style, audience explicitly rather than leaving it implicit | 56 |
| Instructions over constraints | Tell the model what to do, not just what to avoid. Instructions communicate the desired outcome directly; constraints leave the model guessing and can conflict with each other. Reserve constraints for safety/bias prevention or strict format requirements | 56-57 |
| Control max token length | Set a token limit in config, or state a length target in the prompt itself (e.g. "in a tweet length message") | 58 |
| Use variables in prompts | Parameterize reusable prompts (e.g. `{city}`) instead of hardcoding, essential once prompts are embedded in an application | 58 |
| Experiment with input formats/styles | Try the same ask as a question, a statement, and an instruction, results differ | 59 |
| Mix classes in few-shot for classification | Don't group examples by class in the same order every time, the model can overfit to example order rather than learning class features. Start with ~6 few-shot examples and tune from there | 59 |
| Adapt to model updates | Track model version changes and re-test/re-tune prompts against new model capabilities rather than assuming a prompt stays optimal forever | 60 |
| Experiment with output formats | For non-creative tasks (extract, select, parse, order, rank, categorize), request structured output (JSON/XML), forces structure and limits hallucination, and gives you pre-sorted data | 60 |
| Experiment with other prompt engineers | Have multiple people attempt the same prompt following the same best practices, compare variance | 61 |
| CoT-specific: set temperature to 0 | CoT relies on greedy decoding; reasoning chains generally have one correct final answer, so temperature 0 is recommended. Also: the answer must come after the reasoning (order matters, since reasoning tokens change what the model conditions on), and the final answer must be extractable separately from the reasoning text | 61 |
| Document every prompt attempt | Keep a structured log (recommended as a spreadsheet) of every attempt: name/version, goal, model, temperature, token limit, top-K, top-P, full prompt text, full output, plus iteration number and OK/NOT OK/SOMETIMES OK plus feedback. For RAG systems also log query, chunk settings, chunk output. Once stable, move the prompt into the codebase in its own file, separate from application code, and back it with automated tests/evals | 62-63 |

**Documentation template** (Table 21, p.63): Name / Goal / Model / Temperature / Token Limit / Top-K / Top-P / Prompt / Output. This is the same table format used throughout the whitepaper's own worked examples.

## Relevance to system prompts and agent contracts

Paper date: September 2024 (v4). Written for single-turn Vertex AI Studio prompt engineering, pre-dates most agentic frameworks and current-generation prompt caching/extended-thinking features. Read the following with that lens.

- **Directly transferable**: instructions-over-constraints (p.56-57) is one of the strongest, most durable findings here, positive framing ("do X") over negative lists ("don't do Y") applies directly to system prompts and agent tool-use policies, not just one-off asks.
- **Directly transferable**: "design with simplicity" (p.55) and "be specific about the output" (p.56) both generalize cleanly to persistent instructions, an agent's system prompt is read on every turn, so unclear or bloated phrasing compounds across the whole session.
- **Directly transferable**: documenting prompt attempts (p.62-63) maps onto versioning agent system prompts/CLAUDE.md-style files, keep a changelog of what was tried and why, not just the current state.
- **Partially transferable**: role prompting (p.21-23) and system/contextual/role distinctions (p.17-18) map onto agent persona and contract design, but agent definitions usually need more than tone/style, they need scope boundaries, tool permissions and failure-mode handling that this paper doesn't cover (it's about single-shot output framing, not persistent behavioral contracts).
- **Partially transferable**: CoT and self-consistency (p.29-35) are relevant to agent reasoning steps, but current agentic systems often have native extended-thinking or planning modes that supersede manually prompting "let's think step by step."
- **Dated**: the sampling-config guidance (temperature/top-K/top-P starting values, p.8-11) assumes direct API/Studio access to those controls. Most chat-based and agent-harness contexts don't expose per-call sampling knobs to the prompt author, so this section is more relevant to programmatic API use than to system-prompt authoring.
- **Dated**: ReAct via manual LangChain tool loops (p.37-39) predates native tool-use/function-calling APIs and agent SDKs. The reasoning-act-observe loop concept still holds, but the "write your own agent loop in LangChain" mechanics are superseded by first-party tool-calling.
- **Dated/narrow**: Automatic Prompt Engineering (p.40-41) is framed as a manual BLEU/ROUGE scoring workflow, current practice would more likely use LLM-as-judge evals or the model's own scoring, though the core loop (generate variants, evaluate, keep the best) still applies to iterating on system prompts.
- **Not covered but relevant to agents**: this paper has no treatment of tool-definition design, multi-agent coordination, context window/memory management across turns, or guardrails against prompt injection, all of which matter more for persistent agent contracts than for one-shot prompts.
