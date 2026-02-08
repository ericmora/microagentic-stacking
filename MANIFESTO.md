# THE MICROAGENTIC STACKING MANIFESTO

## From Prompt Alchemy to Scalable Software Engineering

## 1. Preamble: The End of the Monolith

We are witnessing the collapse of "Prompt Engineering" as an isolated discipline. The attempt to solve complex business processes through a single giant instruction to a foundational model (LLM) has proven to be a fragile, unpredictable strategy, and impossible to audit at enterprise scale.

Academic research confirmed as early as 2023 that treating LLMs as monolithic black boxes for complex tasks was a dead end [7]. Today, leading institutions like UC Berkeley ratify that the state of the art is no longer achieved with larger individual models, but with "Compound AI Systems" that orchestrate multiple components [13], a trend validated by emerging architectural patterns observed in the industry by leading firms like a16z [15].

AI is not magic; it is probabilistic computation. As such, it must undergo the same engineering disciplines that have allowed software to scale for decades: decoupling, modularity, and strict contracts. The future of AI lies not in larger prompts, but in better system architecture [10].

We propose a radical paradigm shift: stop building monolithic chatbots and start orchestrating compound architectures.

We call this standard **Microagentic Stacking (MAS)**.

## 2. Core Philosophy

Our methodology does not seek to create Artificial General Intelligence (AGI). It seeks to build robust enterprise systems through the orchestration of specialized cognitive units.

We are based on three non-negotiable pillars:

1. **Process Over AI:** The AI does not define the workflow; the business process defines where and how AI is used.
2. **Atomicity Over Generality:** Cognitive complexity is solved by breaking it down into its smallest and indivisible components.
3. **Incremental Growth:** Systems are not designed "finished"; they evolve layer by layer, process by process, from a simple MVP to a complex ecosystem.

## 3. The Technical Principles of MAS

To implement a MAS system, the following architectural laws must be obeyed, inherited from decades of sound software engineering principles:

### I. The Law of the Atomic Microagent (Single Responsibility)

A Microagent must execute a single cognitive task and execute it perfectly. This is the direct application of the Single Responsibility Principle (SRP) to AI components [2]. If an agent tries to "search for information, analyze it, and write a response", it is poorly designed. It must be divided into three distinct agents.

### II. Black Box Isolation (The Black Box Principle)

The internal working of a Microagent is absolutely private and inaccessible to the rest of the system, following microservices design principles and bounded contexts [1].

* The orchestrator does not know what prompt is used internally.
* The orchestrator does not know what model (GPT-4, Claude, local Llama 3) executes the task.

This abstraction allows for refactoring, cost optimization, and changing models within an agent without breaking the upper process.

### III. Radical Decoupling and Contracts (Decoupling via Schema)

Microagents are agnostic to each other. They are governed by the "Design by Contract" methodology, where preconditions and postconditions are strict [3].

* **Rigid Contracts:** Each agent strictly defines what data it accepts (Input Schema) and what data it returns (Output Schema) using standard formats (e.g., JSON Schema, Pydantic).
* **The Orchestrator as Transformer:** It is the exclusive responsibility of the Business Process (the orchestrator) to take the output from Agent A, transform or map the data if necessary, and inject it into Agent B fulfilling its contract.

### IV. Hierarchical and Composable Orchestration

Agents are the pieces, but the value is in the assembly. Complex intelligence does not emerge from a single model, but from the coordination of multiple parts [4].

* **Processes calling Agents:** A workflow orchestrates a sequence of microagents.
* **Processes calling Processes:** A high-level process can invoke another process as if it were just another agent, allowing for infinite recursive composition.

## 4. The Enterprise Governance Agreement

AI autonomy within a company requires strict control. MAS is not just code; it is a framework of responsibility and robustness. ML engineering experts have repeatedly pointed out that the gap between a demo and a system in production lies in the lack of engineering rigor, evaluation, and risk control [14]. Evidence shows that robustness decreases drastically as uncontrolled autonomy increases [8].

### 1. Atomic Accountability

"System error" does not exist. Every generated output must carry an immutable trace signature identifying which specific microagent, which version of the prompt, and which exact model generated it for instant forensic audit.

### 2. Immutability and Versioning (Prompt SemVer)

A prompt is code. It must be version-controlled. Any change to an internal instruction, however small, constitutes a new immutable version of the agent (v1.0 -> v1.1). There are no "hot" changes in production.

### 3. Strict Input Validation (Fail Fast)

We act as strict customs control. Before an agent starts working, the system automatically verifies that the data it is about to receive complies exactly with its input contract. If the data does not fit 100%, the process stops immediately with a visible error. This "Fail Fast" pattern is essential for distributed system stability [5].

### 4. Minimum Contextual Privilege

Information is governed by the "need to know" principle. No agent receives the global context of the operation, only the data strictly necessary for its micro-task. This is critical, as it has been shown that LLM performance degrades significantly when flooded with irrelevant context ("Lost in the Middle phenomenon") [6].

### 5. Unit Economics (FinOps at the Atomic Level)

Cost must be observable per unit. The system must be able to report the exact execution cost of each individual microagent.

## 5. The Quality Framework (Testing Framework)

Since LLMs are probabilistic, testing in MAS must be statistical and multi-level.

* **Level 1: Unit Evals.** Each Microagent must pass a "Golden Dataset" with a defined statistical success threshold (>95%) before being deployed.
* **Level 2: Contract Testing (Integration).** We validate that the pieces fit together using Mocking. We ensure that the orchestrator is correctly transforming data between agents without needing to execute the models.
* **Level 3: Process Testing (E2E).** We validate that the complete business flow meets functional and latency requirements.

## 6. The Three Dimensions of Scalability

In the monolithic paradigm, scaling is expensive and fragile. In MAS, scalability is a natural consequence of architecture.

### I. Technical Scalability: "Stateless by Design"

Our microagents are stateless execution units. This allows deploying from simple architectures to queue-based asynchronous systems (Event-Driven) to manage massive load spikes, without needing to modify the agents' internal logic.

### II. Cognitive Scalability: "Divide and Conquer"

We avoid the cognitive deterioration of long contexts [6]. To solve more complex problems, we do not expand the context; we add more specialized agents to the chain. We maintain constant reliability regardless of problem complexity.

### III. Organizational Scalability: Modular Development

We break the development bottleneck. Thanks to strict contracts and black boxes, multiple teams can work, optimize, and deploy different microagents in parallel without code conflicts and without stopping the ecosystem.

## 7. Reference Architecture: The RFP Engine

To demonstrate the robustness of Microagentic Stacking in a critical environment, we analyze the logical architecture of an Automated Request for Proposal (RFP) Response system. This process requires a strict separation between reasoning (AI) and business data (SQL). The industry is moving towards models where orchestration is managed by explicit state machines, not autonomous loops [9].

### The Microagentic Stack

* **Orchestrator (State Machine):** The core of the system. It is not AI. It is a workflow engine that manages the tender state and directs traffic between agents and databases.
* **Microagent A (Extractor):** Receives raw text from the PDF. Its only mission is to return a structured JSON of technical requirements. It does not opine, only extracts.
* **Integration Layer (Legacy):** The Orchestrator takes the IDs extracted by Agent A and queries the ERP to obtain prices and stock. Key Principle: AI never invents prices.
* **Microagent B (Risk Auditor):** Receives legal clauses. If it detects unacceptable risks, it activates a "Circuit Breaker" [5] and the orchestrator stops the process before drafting.
* **Microagent C (Final Drafter):** Only activates if previous steps are valid. Generates the proposal using exclusively the "clean data" the orchestrator provides.

## 8. Conclusion: Evolution as Standard

Microagentic Stacking is not a static solution; it is a methodology for continuous growth. It allows starting with a simple MVP and evolving into complex ecosystems, adding capabilities and optimizing individual components without risk of regression. The development community at large is adopting this transition from monoliths to agentic workflows as the new paradigm of workload migration [12].

We reject chaos. We embrace structure.
**We don't build demos. We build architecture.**

**Lead Author & Maintainer:** Eric Mora Juan (<ericmora82@gmail.com>)
**Published:** January 2026
This is a living standard. Community contributions are welcome.

## References

### Fundamentals of Software Engineering

1. Newman, S. (2021). Building Microservices: Designing Fine-Grained Systems (2nd Ed.). O'Reilly Media.
2. Martin, R. C. (2017). Clean Architecture: A Craftsman's Guide to Software Structure and Design. Prentice Hall.
3. Meyer, B. (1992). "Applying 'Design by Contract'". Computer, 25(10), 40-51. IEEE. Link: [https://ieeexplore.ieee.org/document/161279](https://ieeexplore.ieee.org/document/161279)
4. Hohpe, G., & Woolf, B. (2003). Enterprise Integration Patterns: Designing, Building, and Deploying Messaging Solutions. Addison-Wesley.
5. Nygard, M. T. (2018). Release It!: Design and Deploy Production-Ready Software (2nd Ed.). Pragmatic Bookshelf.

### AI Systems Research and Architecture (State of the Art)

1. Liu, N. F., et al. (2023). "Lost in the Middle: How Language Models Use Long Contexts". arXiv preprint arXiv:2307.03172. Link: [https://arxiv.org/abs/2307.03172](https://arxiv.org/abs/2307.03172)
2. Khattab, O., et al. (Stanford NLP) (2023). "DSPy: Compiling Declarative Language Model Calls into Self-Improving Pipelines". arXiv preprint arXiv:2310.03714. Link: [https://arxiv.org/abs/2310.03714](https://arxiv.org/abs/2310.03714)
3. Wang, L., et al. (2024). "On the Robustness of Large Language Models for Agentic Tasks". arXiv preprint arXiv:2402.05818. Link: [https://arxiv.org/abs/2402.05818](https://arxiv.org/abs/2402.05818)
4. LangChain Team (2024). "LangGraph: Building Language Agents as Graphs". LangChain Blog. Link: [https://blog.langchain.dev/langgraph/](https://blog.langchain.dev/langgraph/)
5. Husain, H. (2023). "AI Engineering is the New Software Engineering". Hamel's Blog. Link: [https://hamel.dev/blog/posts/ai-eng-is-new-sw-eng/](https://hamel.dev/blog/posts/ai-eng-is-new-sw-eng/)
6. Shopify Engineering (2024). "How Shopify Uses LLMs for Commerce". Shopify Engineering Blog.
7. Daga, D. (Medium). "From Monoliths to Agentic Workflows: The New Paradigm of Workload Migration". Link: [https://medium.com/@dagadeepansh/from-monoliths-to-agentic-workflows-the-new-paradigm-of-workload-migration-6f503f3837cc](https://medium.com/@dagadeepansh/from-monoliths-to-agentic-workflows-the-new-paradigm-of-workload-migration-6f503f3837cc)
8. Berkeley Artificial Intelligence Research (BAIR) (2024). "The Shift from Models to Compound AI Systems". BAIR Blog. Link: [https://bair.berkeley.edu/blog/2024/02/18/compound-ai-systems/](https://bair.berkeley.edu/blog/2024/02/18/compound-ai-systems/)
9. Huyen, C. (2023). "Building LLM applications for production". Chip Huyen's Blog. Link: [https://huyenchip.com/2023/04/11/llm-engineering.html](https://huyenchip.com/2023/04/11/llm-engineering.html)
10. Andreessen Horowitz (a16z) (2023/2024). "Emerging Architectures for LLM Applications". a16z Technology Blog. Link: [https://a16z.com/emerging-architectures-for-llm-applications/](https://a16z.com/emerging-architectures-for-llm-applications/)

### Recent Industry Consensus (2025)

1. Forrester Research (2025). "The Agentic AI Reality Check: Why Governance and Orchestration Will Define the Next Era of Enterprise Automation." (Tech Trends Report).
