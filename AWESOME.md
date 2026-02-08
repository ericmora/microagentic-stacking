# Awesome Microagentic Stacking (MAS) 🚀

A curated list of tools, frameworks, and resources that align with the **[Microagentic Stacking Manifesto](./MANIFESTO.md)**.

> **Criteria for inclusion:** Tools must promote:
>
> 1. **Atomic Design** (Single Responsibility Agents)
> 2. **Strict Contracts** (Schemas, Types, Pydantic)
> 3. **Explicit Orchestration** (Graphs, State Machines, DAGs)
> 4. **Observability** (Tracing, Evals, Replayability)


## 🏗️ Orchestration Frameworks (The "How")

These tools allow you to build deterministic workflows and manage state between agents, avoiding "infinite loops of doom."

* **[LangGraph](https://github.com/langchain-ai/langgraph)** - The gold standard for graph-based agent orchestration. Supports cyclic graphs, persistence, and "human-in-the-loop." Perfectly aligns with MAS Point 3.IV (Hierarchical Orchestration).
* **[Temporal.io](https://temporal.io/)** - Durable execution engine. Ensures that if an agent crashes or waits for days, the state is preserved. Essential for "Atomic Accountability" and reliability in production.
* **[Burr](https://github.com/DAGWorks-Inc/burr)** - A lightweight state machine library for building application state. Framework-agnostic and comes with a great UI to visualize the state transitions (State Machine).
* **[LlamaIndex Workflows](https://docs.llamaindex.ai/en/stable/module_guides/deploying/agents/tools/usage_pattern/)** - Event-driven workflow orchestration. Defines steps and events explicitly, moving away from "magic" recursive agents.

## 🛡️ Contract & Schema Enforcers (The "What")

Tools that enforce **Point 3.III (Design by Contract)**. If it doesn't validate I/O, it doesn't belong here.

* **[PydanticAI](https://github.com/pydantic/pydantic-ai)** - Built by the Pydantic team. Enforces type-safety at runtime. If an agent returns data that doesn't match the schema, it fails fast (MAS Point 4.3).
* **[DSPy](https://github.com/stanfordnlp/dspy)** - **Stanford NLP**. Treats "prompts as code" (or weights). Instead of writing prompt strings, you define **Signatures** (Input/Output contracts) and let the compiler optimize the prompt. The ultimate realization of "Prompt SemVer."
* **[Instructor](https://github.com/jxnl/instructor)** - The pioneer of structured outputs. Patches LLM SDKs to return Pydantic models by default. Simple, effective contract enforcement.

## 🔬 Observability & Evaluation (The "Quality")

Tools for **Point 4.1 (Atomic Accountability)** and **Point 5 (Testing Framework)**.

* **[Langfuse](https://langfuse.com/)** - Open source LLM engineering platform. Traces every step (input/output/latency) and provides a "trace signature" for debugging.
* **[Arize Phoenix](https://phonix.arize.com/)** - AI observability for tracing and evaluating LLM apps. Great for visualizing the "trace" of a request through multiple microagents.
* **[Braintrust](https://www.braintrust.dev/)** - Enterprise-grade logic for "Unit Evals" (MAS Point 5.1). meticulous logging and regression testing for your prompts.
* **[LangSmith](https://smith.langchain.com/)** - From the creators of LangChain/LangGraph. Best-in-class for debugging complex agent graph traversals.

## 🧩 Modular Agent Frameworks

Tools that provide pre-built agents or runtimes, but **MUST** be used with architectural rigor (don't rely on their "magic" defaults).

* **[CrewAI](https://github.com/joaomdmoura/crewAI)** - Popular for role-playing agents. *MAS Note: Use specific Crews as "Microagents" and orchestrate them externally; avoid letting them loop indefinitely.*
* **[Microsoft AutoGen](https://github.com/microsoft/autogen)** - Multi-agent conversation framework. *MAS Note: Use for "group chat" sub-processes where strict determinism is less critical, or use their new graph features.*
* **[Semantic Kernel](https://github.com/microsoft/semantic-kernel)** - Microsoft's SDK. Very strong on "Plugins" (Skills) which function as atomic units. Good for binding code to agents.


## 📚 Educational Resources

* **[The Shift from Models to Compound AI Systems](https://bair.berkeley.edu/blog/2024/02/18/compound-ai-systems/)** - Berkeley AI Research (BAIR). The academic backing for Point 1.
* **[Building Microservices](https://www.oreilly.com/library/view/building-microservices-2nd/9781492034018/)** by Sam Newman. Required reading for understanding *why* we separate concerns.


**[⬆️ Back to Manifesto](./MANIFESTO.md)**
