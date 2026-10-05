---
title: How should one start with AI learning
created: 2026-05-06
updated: 2026-10-05
tags:
  - ai
  - learning
---

# How should one start with AI learning

A learning path for developers and QA engineers. It runs in three tracks, in this order: a plain-language start, Anthropic's courses on working with Claude, then DeepLearning.AI's courses on building, checking and scaling agent work.

Each course is marked ✅ (done), 🚧 (in progress) or ⬜ (planned). Each course sits in a table with a short summary and my takeaways, with a link to my notes where they exist.

## How the path is ordered

| Stage | Principle | Where it shows up |
| ----- | --------- | ----------------- |
| 1 | Learn to talk to the model before you learn to build with it. | Track 1 |
| 2 | Learn the collaboration habits (the 4Ds) before the tools, so the tools do not set your habits. | AI Fluency, early in Track 2 |
| 3 | Learn one tool deeply (Claude Code), then extend it: skills, MCP, subagents. | Track 2 |
| 4 | Move from one person to a team: workflow, specs, review, evaluation. | End of Track 2, then Track 3 |
| 5 | Go to the theory of agents last, once you have something to compare it with. | Agentic AI, late in Track 3 |

## Track 1: AI for Everyone

Goal: get comfortable with what AI can and cannot do, and write prompts that work. No coding needed. Everyone on the team, QA included, starts here. Take these in order: the first gives the vocabulary, the second the practical skill.

|     | Course | Summary | My Takeaways |
| --- | ------ | ------- | ------------ |
| ✅ | [AI for Everyone](https://www.deeplearning.ai/courses/ai-for-everyone) (DeepLearning.AI) | My first AI course. The vocabulary and the business view of AI, without code. | AI, machine learning, deep learning, data science and generative AI are different things, and an LLM is one kind of ML model. ML maps an input to an output and works best on a simple concept with lots of data. Supervised learning needs manually labelled data. Garbage in, garbage out. AI team roles: software engineer, ML engineer, data engineer, AI product manager. Transformation playbook: pilots first, then an in-house team, broad training, a strategy, and communication. |
| ✅ | [AI Prompting for Everyone](https://www.deeplearning.ai/courses/ai-prompting-for-everyone) (DeepLearning.AI) | The prompting basics: be specific, give context, state the format you want, iterate. | The habits behind this course are the Description competency of the 4Ds: [[ai-fluency/Description\|Description]]. |
| ⬜ | [Generative AI for Everyone](https://www.deeplearning.ai/courses/generative-ai-for-everyone) (DeepLearning.AI) | A beginner overview of generative AI. | Not taken. AI for Everyone already covered my starting point, but it is a good next step for anyone new. |

## Track 2: Courses from Anthropic

Goal: work well with Claude, then with Claude Code, then extend it. Anthropic Academy: [academy.claude.com](https://academy.claude.com).

Take these in order.

|     | Course                                                                                                                                    | Summary                                                                                                    | My Takeaways                                                                                                                                                                                                                                            |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ✅   | [Claude 101](https://academy.claude.com/courses/claude-101) | The product tour: projects, files, connectors, and how to get real work out of Claude.                     | No separate notes.                                                                                                                                                                                                                                      |
| ✅   | [AI Fluency: Framework & Foundations](https://academy.claude.com/courses/ai-fluency-framework-foundations)                                    | The 4D framework: Delegation, Description, Discernment, Diligence.                                         | AI is a thinking partner, not a vending machine. Notes: [[ai-fluency/index\|AI Fluency]], [[ai-fluency/Delegation\|Delegation]], [[ai-fluency/Description\|Description]], [[ai-fluency/Discernment\|Discernment]], [[ai-fluency/Diligence\|Diligence]]. |
| ✅   | [Claude Code in Action](https://academy.claude.com/courses/claude-code-in-action)                                                         | Using Claude Code on a real codebase.                                                                      | Notes: [[ai-fundamentals/what-is-the-harness\|What is the harness]], [[ai-fundamentals/what-is-an-ai-agent\|What is an AI agent]].                                                                                                                      |
| ✅   | [Introduction to Agent Skills](https://academy.claude.com/courses/introduction-to-agent-skills) | Packaging a repeatable way of working so Claude applies it every time.                                     | Notes: [[ai-fundamentals/what-is-a-skill\|What is a skill]], [[ai-fundamentals/skills-vs-agents\|Skills vs agents]].                                                                                                                                    |
| ✅   | [Introduction to Model Context Protocol](https://academy.claude.com/courses/introduction-to-model-context-protocol) | How MCP servers expose tools, resources and prompts to a client.                                           | MCP is not "just an API". It is three primitives (tools, resources, prompts) on top of any transport, and prompts turn a loose request into a structured workflow.                                                                                      |
| ✅   | [Introduction to Subagents](https://academy.claude.com/courses/introduction-to-subagents) | Delegating work to focused helpers with their own context.                                                 | Notes: [[ai-fundamentals/sub-agents\|Sub-agents]].                                                                                                                                                                                                      |
| 🚧  | [The AI-Native SDLC Playbook](https://academy.claude.com/courses/ai-native-sdlc-playbook)                                                | How to change planning, review, testing and deployment around Claude Code, not only how code gets written. | In progress. Likely the most relevant course for QA.                                                                                                                                                                                                    |
| ⬜   | [Building Effective Human Agent Teams](https://academy.claude.com/courses/building-effective-human-agent-teams) (beta) | From one person using AI to a team using it.                                                               | Not taken yet.                                                                                                                                                                                                                                          |
| ⬜   | [AI Capabilities and Limitations](https://academy.claude.com/courses/ai-capabilities-and-limitations) | Where AI works and where it fails.                                                                         | Not taken yet. Also a good first course for cautious groups.                                                                                                                                                                                            |
| ⬜   | [Model Context Protocol: Advanced Topics](https://academy.claude.com/courses/model-context-protocol-advanced-topics) | The next level after the introduction.                                                                     | Not taken yet. Take it after you have used MCP for a while.                                                                                                                                                                                             |

## Track 3: Courses from DeepLearning.AI

Goal: the engineering side. Specs, review, evaluation, and the theory of agents. Courses at [deeplearning.ai](https://www.deeplearning.ai).

Take these in order, after the first six Anthropic courses, because they assume you can already drive a coding agent.

|     | Course | Summary | My Takeaways |
| --- | ------ | ------- | ------------ |
| ✅ | [Agent Skills with Anthropic](https://www.deeplearning.ai/short-courses/agent-skills-with-anthropic/) | A hands-on course on building skills. | A second pass on the Anthropic skills course. See [[ai-fundamentals/what-is-a-skill\|What is a skill]]. |
| ⬜ | [Spec-Driven Development with Coding Agents](https://www.deeplearning.ai/courses/spec-driven-development-with-coding-agents) (with JetBrains) | Write a spec first, then plan, implement and verify with an agent. | Not started. Developers start here. |
| ⬜ | [AI Code Review](https://www.deeplearning.ai/short-courses/ai-code-review/) | Reviewing agent-written code. | Not taken yet. Useful for developers and QA. |
| ⬜ | [Evaluating AI Agents](https://www.deeplearning.ai/short-courses/evaluating-ai-agents/) | How to test something that gives a different answer each time. | Not taken yet. QA should take this one. |
| ⬜ | [LLM Evaluation Course (Practice)](https://www.evidentlyai.com/llm-evaluation-course-practice) (Evidently AI, not DeepLearning.AI) | Hands-on evaluation of LLM output. | Not taken yet. Pairs with Evaluating AI Agents, so QA can take it right after. |
| ⬜ | [Agentic AI](https://www.deeplearning.ai/courses/agentic-ai/) (about 10 hours) | The conceptual backbone of agentic systems. | Not taken yet. The longest course, so it comes late. |
| ⬜ | [Practical Multi AI Agents and Advanced Use Cases with crewAI](https://www.deeplearning.ai/short-courses/practical-multi-ai-agents-and-advanced-use-cases-with-crewai/) | Multi-agent orchestration outside Anthropic's tooling. | Not taken yet. A second point of view. |

## Suggested path by role

| Step | Developer | QA |
| --- | --- | --- |
| Start | Track 1, then Track 2 up to Agent Skills | Track 1, then Claude 101 and AI Fluency |
| Build skill | Track 2 from MCP to the SDLC Playbook, then Agent Skills with Anthropic and Spec-Driven Development | The SDLC Playbook and AI Capabilities and Limitations, then AI Code Review |
| Go deeper | AI Code Review, Evaluating AI Agents, Agentic AI | Evaluating AI Agents, LLM Evaluation, Agentic AI |

## What I left out

Generative AI for Everyone's overlap with AI for Everyone, DeepLearning.AI's Claude Code course (covered by Claude Code in Action and Claude 101), product management certifications, n8n tutorials, machine learning and deep learning specialisations, maths for ML, inference and serving courses, and fine-tuning courses. They are for people who train models. This path is for people who use them and build on them.
