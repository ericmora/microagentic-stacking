# THE MICROAGENTIC STACKING MANIFESTO

> 注意：本翻译由 Gemini 3 自动完成。

## 从提示词炼金术到可扩展的软件工程

---

## 1. 序言：单体架构的终结

我们正在目睹“提示词工程（Prompt Engineering）”作为一门孤立学科的崩溃。企图通过对基础模型（LLM）发出一行巨大的指令来解决复杂的业务流程，已被证明是一种脆弱、不可预测且在企业规模上无法审计的策略。

学术研究早在2023年就证实，将LLM视为处理复杂任务的单体黑盒是一条死胡同 [7]。今天，像加州大学伯克利分校这样的领先机构证实，最先进的技术不再是通过更大的单一模型实现的，而是通过编排多个组件的“复合AI系统（Compound AI Systems）”实现的 [13]，这一趋势得到了a16z等领先公司在行业中观察到的新兴架构模式的验证 [15]。

AI不是魔法，它是概率计算。因此，它必须服从于几十年来让软件得以扩展的相同工程学科：解耦、模块化和严格的契约。AI的未来不在于更大的提示词，而在于更好的系统架构 [10]。

我们提出了一个根本性的范式转变：停止构建单体聊天机器人，开始编排复合架构。

我们将此标准称为 **微智能体堆叠（Microagentic Stacking，MAS）**。

---

## 2. 核心理念

我们的方法论不寻求创造通用人工智能（AGI）。它寻求通过编排专门的认知单元来构建稳健的企业系统。

我们基于三个不可协商的支柱：

1. **流程至上：** AI不定义工作流；业务流程定义在哪里以及如何使用AI。
2. **原子性重于通用性：** 通过将认知复杂性分解为其最小和不可分割的组件来解决它。
3. **增量增长：** 系统不是设计成“完成”的；它们是一层一层、一个过程一个过程地演变的，从简单的MVP到复杂的生态系统。

---

## 3. MAS的技术原则

实施MAS系统，必须遵守以下架构定律，这些定律继承自数十年来稳健的软件工程原则：

### I. 原子微智能体定律（单一职责）

一个微智能体必须执行单一的认知任务，并完美地执行它。这是单一职责原则（SRP）在AI组件上的直接应用 [2]。如果一个智能体试图“搜索信息，分析它并撰写回复”，那么它的设计就很糟糕。它必须被分成三个不同的智能体。

### II. 黑盒隔离（黑盒原则）

微智能体的内部运作对于系统的其余部分是绝对私有和不可访问的，遵循微服务设计原则和限界上下文 [1]。

* 编排器不知道内部使用了什么提示词。
* 编排器不知道通过什么模型（GPT-4、Claude、本地Llama 3）执行任务。

这种抽象允许在不破坏上层流程的情况下，在智能体内部进行重构、成本优化和更改模型。

### III. 彻底解耦与契约（通过Schema解耦）

微智能体之间是不可知的。它们受“契约式设计”方法论的约束，其中前置条件和后置条件是严格的 [3]。

* **严格契约 (Rigid Contracts)：** 每个代理严格定义它接受什么数据 (Input Schema) 和返回什么数据 (Output Schema)，使用标准格式（例如 JSON Schema, Pydantic）。
* **作为转换器的编排器：** 业务流程（编排器）的唯一责任是获取智能体A的输出，在必要时转换或映射数据，并在满足智能体B契约的情况下将其注入智能体B。

### IV. 分层与可组合的编排

智能体是零件，但价值在于组装。复杂的智能不是从单一模型中涌现的，而是从多个部分的协调中涌现的 [4]。

* **调用智能体的流程：** 工作流编排一系列微智能体。
* **调用流程的流程：** 一个高级流程可以像调用另一个智能体一样调用另一个流程，允许无限的递归组合。

---

## 4. 企业治理协议

企业内AI的自主性需要严格的控制。MAS不仅仅是代码；它是一个责任和稳健性的框架。机器学习工程专家多次指出，演示版和生产系统之间的差距在于缺乏工程严谨性、评估和风险控制 [14]。证据表明，随着不受控制的自主性增加，稳健性急剧下降 [8]。

### 1. 原子可追溯性（Atomic Accountability）

“系统错误”不存在。每个生成的输出必须携带不可变的追踪签名 (immutable trace signature)，标识具体是哪个微代理、哪个版本的提示词以及哪个确切的模型生成了它，以便进行即时取证审计。

### 2. 不可变性与版本控制（Prompt SemVer）

提示词就是代码。它必须受版本控制。内部指令的任何变更，无论多么微小，都构成了代理的一个新的不可变版本 (v1.0 -> v1.1)。生产环境中不存在“热”更 改。

### 3. 接入口的严格验证（Fail Fast）

我们充当严格的海关控制。在智能体开始工作之前，系统会自动验证它将接收的数据是否完全符合其输入契约。如果数据不是100%匹配，该过程将立即停止并显示可见错误。这种“快速失败（Fail Fast）”模式对于分布式系统的稳定性至关重要 [5]。

### 4. 最小上下文特权

信息受“需知（need to know）”原则支配。没有智能体接收操作的全局上下文，只接收其微任务严格需要的数据。这很关键，因为已经证明，当被无关的上下文淹没时，LLM的性能会显著下降（“迷失在中间现象”） [6]。

### 5. 单元经济（原子级别的FinOps）

成本必须按单位可观察。系统必须能够报告每个单独微智能体的确切执行成本。

---

## 5. 质量框架（测试框架）

由于LLM是概率性的，MAS中的测试必须是统计性的和多层次的。

* **第1级：单元评估（Unit Evals）。** 每个微智能体在部署前必须通过具有定义的统计成功阈值（>95%）的“黄金数据集”测试。
* **第2级：契约测试（集成）。** 我们使用Mocking验证各个部分是否通过。我们确保编排器在智能体之间正确转换数据，而无需执行模型。
* **第3级：流程测试（E2E）。** 我们验证完整的业务流程是否符合功能和延迟要求。

---

## 6. 扩展性的三个维度

在单体范式中，扩展昂贵且脆弱。在MAS中，扩展性是架构的自然结果。

### I. 技术扩展性：“设计上无状态”

我们的微智能体是无状态（stateless）执行单元。这允许从简单的架构部署到基于队列的异步系统（事件驱动），以管理大规模的负载峰值，而无需修改智能体的内部逻辑。

### II. 认知扩展性：“分而治之”

我们避免长上下文的认知恶化 [6]。为了解决更复杂的问题，我们不扩展上下文；我们在链中添加更多专门的智能体。无论问题的复杂性如何，我们都保持恒定的可靠性。

### III. 组织扩展性：模块化开发

我们打破了开发的瓶颈。由于严格的契约和黑盒，多个团队可以并行工作、优化和部署不同的微智能体，而没有代码冲突，也不会停止生态系统。

---

## 7. 参考架构：RFP引擎（招标书引擎）

为了展示微智能体堆叠在关键环境中的稳健性，我们分析了一个自动招标书（RFP）响应系统的逻辑架构。该过程需要推理（AI）和业务数据（SQL）之间的严格分离。行业正向由显式状态机而非自主循环管理编排的模型转变 [9]。

### 微智能体堆栈

* **编排器（状态机）：** 系统的核心。它不是AI。它是一个工作流引擎，管理招标状态并指导智能体和数据库之间的流量。
* **微智能体A（提取器）：** 从PDF接收原始文本。它的唯一任务是返回技术要求的结构化JSON。它不发表意见，只负责提取。
* **集成层（传统）：** 编排器获取智能体A提取的ID，并查询ERP以获取价格和库存。关键原则：AI从不编造价格。
* **微智能体B（风险审计员）：** 接收法律条款。如果检测到不可接受的风险，它会激活“断路器（Circuit Breaker）”[5]，编排器会在起草前停止该过程。
* **微智能体C（最终起草者）：** 仅在前面的步骤有效时才激活。仅使用编排器提供的“干净数据”生成提案。

---

## 8. 结论：进化作为标准

微智能体堆叠不是一个静态的解决方案；它是一种持续增长的方法论。它允许从简单的MVP开始，演变成复杂的生态系统，在没有回归风险的情况下增加能力和优化单个组件。整个开发社区正在采纳这种从单体到智能体工作流的过渡，作为工作负载迁移的新范式 [12]。

我们拒绝混乱。我们拥抱结构。
**我们不构建Demo。我们构建架构。**

**主要作者 & 维护者：** Eric Mora Juan (<ericmora82@gmail.com>)
**发布时间：** 2026年1月
这是一个活的标准。欢迎社区贡献。

---

## 参考文献

### 软件工程基础

1. Newman, S. (2021). Building Microservices: Designing Fine-Grained Systems (2nd Ed.). O'Reilly Media.
2. Martin, R. C. (2017). Clean Architecture: A Craftsman's Guide to Software Structure and Design. Prentice Hall.
3. Meyer, B. (1992). "Applying 'Design by Contract'". Computer, 25(10), 40-51. IEEE. Link: [https://ieeexplore.ieee.org/document/161279](https://ieeexplore.ieee.org/document/161279)
4. Hohpe, G., & Woolf, B. (2003). Enterprise Integration Patterns: Designing, Building, and Deploying Messaging Solutions. Addison-Wesley.
5. Nygard, M. T. (2018). Release It!: Design and Deploy Production-Ready Software (2nd Ed.). Pragmatic Bookshelf.

### AI系统研究与架构（最新技术）

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

### 近期行业共识（2025）

1. Forrester Research (2025). "The Agentic AI Reality Check: Why Governance and Orchestration Will Define the Next Era of Enterprise Automation." (Tech Trends Report).
