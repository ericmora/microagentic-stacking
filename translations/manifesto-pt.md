# THE MICROAGENTIC STACKING MANIFESTO

> Nota: Esta tradução foi realizada automaticamente pelo Gemini 3.

## Da Alquimia dos Prompts à Engenharia de Software Escalável

---

## 1. Preâmbulo: O Fim do Monólito

Estamos a assistir ao colapso do "Prompt Engineering" como disciplina isolada. A tentativa de resolver processos de negócio complexos através de uma única instrução gigante a um modelo fundacional (LLM) provou ser uma estratégia frágil, imprevisível e impossível de auditar à escala empresarial.

A investigação académica já confirmava em 2023 que tratar os LLMs como caixas negras monolíticas para tarefas complexas era um beco sem saída [7]. Hoje, instituições líderes como a UC Berkeley ratificam que o estado da arte já não se alcança com modelos individuais maiores, mas com "Sistemas Compostos de IA" que orquestram múltiplos componentes [13], uma tendência validada pelos padrões de arquitetura emergentes observados na indústria por firmas líderes como a16z [15].

A IA não é magia; é computação probabilística. Como tal, deve submeter-se às mesmas disciplinas de engenharia que permitiram escalar o software durante décadas: desacoplamento, modularidade e contratos estritos. O futuro da IA não está em prompts maiores, mas numa melhor arquitetura de sistemas [10].

Propomos uma mudança de paradigma radical: deixar de construir chatbots monolíticos e começar a orquestrar arquiteturas compostas.

A este padrão chamamos **Microagentic Stacking (MAS)**.

---

## 2. Filosofia Central

A nossa metodologia não procura criar uma Inteligência Artificial Geral (AGI). Procura construir sistemas empresariais robustos através da orquestração de unidades cognitivas especializadas.

Baseamo-nos em três pilares inegociáveis:

1. **O Processo Manda:** A IA não define o fluxo de trabalho; o processo de negócio define onde e como a IA é utilizada.
2. **Atomicidade sobre Generalidade:** A complexidade cognitiva resolve-se dividindo-a nos seus componentes mais pequenos e indivisíveis.
3. **Crescimento Incremental:** Os sistemas não se desenham "finalizados"; evoluem camada a camada, processo a processo, desde um MVP simples até um ecossistema complexo.

---

## 3. Os Princípios Técnicos do MAS

Para implementar um sistema MAS, devem obedecer-se às seguintes leis de arquitetura, herdadas de décadas de princípios sólidos de engenharia de software:

### I. A Lei do Microagente Atómico (Single Responsibility)

Um Microagente deve executar uma única tarefa cognitiva e executá-la perfeitamente. Esta é a aplicação direta do Princípio de Responsabilidade Única (SRP) aos componentes de IA [2]. Se um agente tenta "procurar informação, analisá-la e redigir uma resposta", está mal desenhado. Deve dividir-se em três agentes distintos.

### II. O Isolamento de Caixa Negra (The Black Box Principle)

O funcionamento interno de um Microagente é absolutamente privado e inacessível para o resto do sistema, seguindo os princípios de design de microsserviços e contextos delimitados [1].

* O orquestrador não sabe que prompt é utilizado internamente.
* O orquestrador não sabe que modelo (GPT-4, Claude, Llama 3 local) executa a tarefa.

Esta abstração permite refatorizar, otimizar custos e mudar modelos dentro de um agente sem quebrar o processo superior.

### III. Desacoplamento Radical e Contratos (Decoupling via Schema)

Os Microagentes são agnósticos entre si. Regem-se pela metodologia de "Design por Contrato", onde as pré-condições e pós-condições são estritas [3].

* **Contratos Rígidos:** Cada agente define estritamente quais dados aceita (Input Schema) e quais dados retorna (Output Schema) usando formatos padrão (p. ex., JSON Schema, Pydantic).
* **O Orquestrador como Transformador:** É responsabilidade exclusiva do Processo de Negócio (o orquestrador) tomar a saída do Agente A, transformar ou mapear os dados se for necessário, e injetá-los no Agente B cumprindo o seu contrato.

### IV. Orquestração Hierárquica e Componível

Os agentes são as peças, mas o valor está na montagem. A inteligência complexa não emerge de um único modelo, mas da coordenação de múltiplas partes [4].

* **Processos que chamam Agentes:** Um fluxo de trabalho orquestra uma sequência de microagentes.
* **Processos que chamam Processos:** Um processo de alto nível pode invocar outro processo como se fosse apenas mais um agente, permitindo uma composição recursiva infinita.

---

## 4. O Acordo de Governança Empresarial

A autonomia da IA dentro de uma empresa requer um controlo estrito. MAS não é apenas código; é um quadro de responsabilidade e robustez. Especialistas em engenharia de ML assinalaram reiteradamente que a brecha entre uma demo e um sistema em produção reside na falta de rigor de engenharia, avaliação e controlo de riscos [14]. A evidência mostra que a robustez diminui drasticamente à medida que aumenta a autonomia não controlada [8].

### 1. Rastreabilidade Atómica (Atomic Accountability)

O erro "de sistema" não existe. Cada output gerado deve carregar uma assinatura de rastreio imutável que identifique qual microagente específico, qual versão do prompt e qual modelo exato o gerou para uma auditoria forense instantânea.

### 2. Imutabilidade e Versionamento (Prompt SemVer)

Um prompt é código. Deve estar sob controle de versão. Qualquer mudança numa instrução interna, por menor que seja, constitui uma nova versão imutável do agente (v1.0 -> v1.1). Não existem mudanças "a quente" em produção.

### 3. Validação Estrita na Entrada (Fail Fast)

Atuamos como um controlo aduaneiro estrito. Antes de um agente começar a trabalhar, o sistema verifica automaticamente que os dados que vai receber cumprem exatamente com o seu contrato de entrada. Se os dados não encaixam a 100%, o processo para imediatamente com um erro visível. Este padrão de "Fail Fast" é essencial para a estabilidade de sistemas distribuídos [5].

### 4. Mínimo Privilégio Contextual

A informação rege-se pelo princípio de "necessidade de saber". Nenhum agente recebe o contexto global da operação, apenas os dados estritamente necessários para a sua microtarefa. Isto é crítico, já que se demonstrou que o rendimento dos LLMs se degrada significativamente quando inundados com contexto irrelevante ("Lost in the Middle phenomenon") [6].

### 5. Economia Unitária (FinOps at the Atomic Level)

O custo deve ser observável por unidade. O sistema deve ser capaz de reportar o custo exato de execução de cada microagente individual.

---

## 5. O Quadro de Qualidade (Testing Framework)

Dado que os LLMs são probabilísticos, o testing em MAS deve ser estatístico e multinível.

* **Nível 1: Avaliações Unitárias (Unit Evals).** Cada Microagente deve superar um "Golden Dataset" com um limiar de sucesso estatístico definido (>95%) antes de ser implantado.
* **Nível 2: Testing de Contrato (Integration).** Validamos que as peças encaixam mediante Mocking. Asseguramos que o orquestrador está a transformar corretamente os dados entre agentes sem necessidade de executar os modelos.
* **Nível 3: Testing de Processo (E2E).** Validamos que o fluxo de negócio completo cumpre com os requisitos funcionais e de latência.

---

## 6. As Três Dimensões da Escalabilidade

No paradigma monolítico, escalar é custoso e frágil. Em MAS, a escalabilidade é uma consequência natural da arquitetura.

### I. Escalabilidade Técnica: "Stateless por Design"

Os nossos microagentes são unidades de execução sem estado (stateless). Isto permite implantar desde arquiteturas simples até sistemas assíncronos baseados em filas (Event-Driven) para gerir picos de carga massivos, sem necessidade de modificar a lógica interna dos agentes.

### II. Escalabilidade Cognitiva: "Dividir e Conquistar"

Evitamos a deterioração cognitiva dos contextos longos [6]. Para resolver problemas mais complexos, não ampliamos o contexto; adicionamos mais agentes especializados à cadeia. Mantemos a fiabilidade constante independentemente da complexidade do problema.

### III. Escalabilidade Organizacional: Desenvolvimento Modular

Quebramos o gargalo do desenvolvimento. Graças aos contratos estritos e caixas negras, múltiplas equipas podem trabalhar, otimizar e implantar diferentes microagentes em paralelo sem conflitos de código e sem parar o ecossistema.

---

## 7. Arquitetura de Referência: O Motor de Licitações (RFP Engine)

Para demonstrar a robustez do Microagentic Stacking num ambiente crítico, analisamos a arquitetura lógica de um sistema de Resposta Automática a Licitações (RFPs). Este processo requer uma estrita separação entre o raciocínio (IA) e os dados de negócio (SQL). A indústria move-se para modelos onde a orquestração se gere mediante máquinas de estado explícitas, não mediante loops autónomos [9].

### A Pilha Microagêntica (The Stack)

* **Orquestrador (State Machine):** O núcleo do sistema. Não é IA. É um motor de fluxo de trabalho que gere o estado da licitação e dirige o tráfego entre agentes e bases de dados.
* **Microagente A (Extrator):** Recebe texto cru do PDF. A sua única missão é devolver um JSON estruturado de requisitos técnicos. Não opina, apenas extrai.
* **Camada de Integração (Legacy):** O Orquestrador toma os IDs extraídos pelo Agente A e consulta o ERP para obter preços e stock. Princípio Chave: A IA nunca inventa preços.
* **Microagente B (Auditor de Risco):** Recebe as cláusulas legais. Se deteta riscos inaceitáveis, ativa um "Disjuntor" (Circuit Breaker) [5] e o orquestrador para o processo antes da redação.
* **Microagente C (Redator Final):** Apenas se ativa se os passos anteriores forem válidos. Gera a proposta utilizando exclusivamente os "dados limpos" que o orquestrador lhe proporciona.

---

## 8. Conclusão: A Evolução como Padrão

Microagentic Stacking não é uma solução estática; é uma metodologia para o crescimento contínuo. Permite começar com um MVP simples e evoluir para ecossistemas complexos, adicionando capacidades e otimizando componentes individuais sem risco de regressão. A comunidade de desenvolvimento em geral está a adotar esta transição desde monólitos para fluxos de trabalho agênticos como o novo paradigma de migração de cargas de trabalho [12].

Rejeitamos o caos. Abraçamos a estrutura.
**Não construímos demos. Construímos arquitetura.**

**Autor Principal & Mantenedor:** Eric Mora Juan (<ericmora82@gmail.com>)
**Publicado:** Janeiro 2026
Este é um padrão vivo. As contribuições da comunidade são bem-vindas.

---

## Referências

### Fundamentos de Engenharia de Software

1. Newman, S. (2021). Building Microservices: Designing Fine-Grained Systems (2nd Ed.). O'Reilly Media.
2. Martin, R. C. (2017). Clean Architecture: A Craftsman's Guide to Software Structure and Design. Prentice Hall.
3. Meyer, B. (1992). "Applying 'Design by Contract'". Computer, 25(10), 40-51. IEEE. Link: [https://ieeexplore.ieee.org/document/161279](https://ieeexplore.ieee.org/document/161279)
4. Hohpe, G., & Woolf, B. (2003). Enterprise Integration Patterns: Designing, Building, and Deploying Messaging Solutions. Addison-Wesley.
5. Nygard, M. T. (2018). Release It!: Design and Deploy Production-Ready Software (2nd Ed.). Pragmatic Bookshelf.

### Investigação e Arquitetura de Sistemas de IA (Estado da Arte)

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

### Consenso Industrial Recente (2025)

1. Forrester Research (2025). "The Agentic AI Reality Check: Why Governance and Orchestration Will Define the Next Era of Enterprise Automation." (Relatório de Tendências Tecnológicas).
