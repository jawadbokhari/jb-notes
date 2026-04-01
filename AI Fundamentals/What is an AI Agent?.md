---
title: What is an AI Agent?
parent: AI Fundamentals
---

AI Agent
A system built around an LLM. 
A system that perceives its environment, make decisions, and take actions to achieve a goals. An agent has the brain (usually but not always an LLM - fuzzy logic, ML models, rule-based systems)

[[LLMs-vs-Agents.excalidraw]]

Agents mimic human decision-making. They are built with 4 core modules. 
1. Brain ("Model") - the LLM that handles reasoning, planning, and natural language understanding.
2. Memory - stores past interactions and successes. 
	1. short-term memory keeps tracks of current tasks
	2. long-term memory helps the agent learn and adapt over time.
3. Planning - the ability to decompose a problem into a sequence of steps. Different frameworks (not going into details yet)
	1. Task Decomposition
	2. Chain-of-thoughts
	3. Tree-of-Thoughts
	4. ReAct 
4. Tools - External APIs and software that allows the agent to interact with the world. Access to the web, calculator, any application, script, or an interpreter application, etc.

### Practical Examples: 
 - Customer Support agent: handles customer queries and trouble tickets. 
 - Software Developer: Develops software applications
 - Technical Writer: 
 - other examples? 

### Can they learn and adapt? 
LLMs are frozen - no change over time. How agents handle the memory/state? 
 - **Short-term memory**: (Context-window) A short-term memory of ongoing conversation that is ended when a conversation is ended. 
	- For each request to LLM, the context window is passed to LLM
	- Different LLMs support different window sizes: 
- **Long-term memory**: a vector or graph database containing facts, user profiles, etc to "recall" relevant information when needed. (Memory tool vs RAG) - keep it for some other time