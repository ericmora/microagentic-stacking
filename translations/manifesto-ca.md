# THE MICROAGENTIC STACKING MANIFESTO

> Nota: Aquesta traducció ha estat realitzada automàticament per Gemini 3.

## De l'Alquímia dels Prompts a l'Enginyeria de Software Escalable


## 1. Preàmbul: La Fi del Monòlit

Estem presenciant el col·lapse del "Prompt Engineering" com a disciplina aïllada. L'intent de resoldre processos de negoci complexos mitjançant una única instrucció gegant a un model fundacional (LLM) ha demostrat ser una estratègia fràgil, imprevisible i impossible d'auditar a escala empresarial.

La investigació acadèmica ja confirmava el 2023 que tractar els LLMs com a caixes negres monolítiques per a tasques complexes era un carreró sense sortida [7]. Avui, institucions líders com la UC Berkeley ratifiquen que l'estat de l'art ja no s'aconsegueix amb models individuals més grans, sinó amb "Sistemes Compostos d'IA" que orquestren múltiples components [13], una tendència validada pels patrons d'arquitectura emergents observats a la indústria per firmes líders com a16z [15].

La IA no és màgia; és còmput probabilístic. Com a tal, s'ha de sotmetre a les mateixes disciplines d'enginyeria que han permès escalar el software durant dècades: desacoblament, modularitat i contractes estrictes. El futur de la IA no està en prompts més grans, sinó en una millor arquitectura de sistemes [10].

Proposem un canvi de paradigma radical: deixar de construir chatbots monolítics i començar a orquestrar arquitectures compostes.

A aquest estàndard l'anomenem **Microagentic Stacking (MAS)**.


## 2. Filosofia Central

La nostra metodologia no busca crear una Intel·ligència Artificial General (AGI). Busca construir sistemes empresarials robustos mitjançant l'orquestració d'unitats cognitives especialitzades.

Ens basem en tres pilars innegociables:

1. **El Procés Mana:** La IA no defineix el flux de treball; el procés de negoci defineix on i com s'utilitza la IA.
2. **Atomicitat sobre Generalitat:** La complexitat cognitiva es resol dividint-la en els seus components més petits i indivisibles.
3. **Creixement Incremental:** Els sistemes no es dissenyen "finalitzats"; evolucionen capa a capa, procés a procés, des d'un MVP simple fins a un ecosistema complex.


## 3. Els Principis Tècnics del MAS

Per implementar un sistema MAS, s'han d'obeir les següents lleis d'arquitectura, heretades de dècades de principis sòlids d'enginyeria de software:

### I. La Llei del Microagent Atòmic (Single Responsibility)

Un Microagent ha d'executar una sola tasca cognitiva i executar-la perfectament. Aquesta és l'aplicació directa del Principi de Responsabilitat Única (SRP) als components d'IA [2]. Si un agent intenta "buscar informació, analitzar-la i redactar una resposta", està mal dissenyat. S'ha de dividir en tres agents diferents.

### II. L'Aïllament de Caixa Negra (The Black Box Principle)

El funcionament intern d'un Microagent és absolutament privat i inaccessible per a la resta del sistema, seguint els principis de disseny de microserveis i contextos delimitats [1].

* L'orquestrador no sap quin prompt s'utilitza internament.
* L'orquestrador no sap quin model (GPT-4, Claude, Llama 3 local) executa la tasca.

Aquesta abstracció permet refactoritzar, optimitzar costos i canviar models dins d'un agent sense trencar el procés superior.

### III. Desacoblament Radical i Contractes (Decoupling via Schema)

Els Microagents són agnòstics entre si. Es regeixen per la metodologia de "Disseny per Contracte", on les precondicions i postcondicions són estrictes [3].

* **Contractes Rígids:** Cada agent defineix estrictament quines dades accepta (Input Schema) i quines dades retorna (Output Schema) usant formats estàndard (p. ex., JSON Schema, Pydantic).
* **L'Orquestrador com a Transformador:** És responsabilitat exclusiva del Procés de Negoci (l'orquestrador) prendre la sortida de l'Agent A, transformar o mapejar les dades si és necessari, i injectar-les a l'Agent B complint el seu contracte.

### IV. Orquestració Jeràrquica i Composable

Els agents són les peces, però el valor està en l'assemblatge. La intel·ligència complexa no emergeix d'un sol model, sinó de la coordinació de múltiples parts [4].

* **Processos que criden Agents:** Un flux de treball orquestra una seqüència de microagents.
* **Processos que criden Processos:** Un procés d'alt nivell pot invocar un altre procés com si fos un agent més, permetent una composició recursiva infinita.


## 4. L'Acord de Governança Empresarial

L'autonomia de la IA dins d'una empresa requereix un control estricte. MAS no és només codi; és un marc de responsabilitat i robustesa. Experts en enginyeria de ML han assenyalat reiteradament que la bretxa entre una demo i un sistema en producció resideix en la falta de rigor d'enginyeria, avaluació i control de riscos [14]. L'evidència mostra que la robustesa disminueix dràsticament a mesura que augmenta l'autonomia no controlada [8].

### 1. Traçabilitat Atòmica (Atomic Accountability)

L'error "del sistema" no existeix. Cada output generat ha de portar una signatura de traça immutable que identifiquin quin microagent específic, quina versió del prompt i quin model exacte el va generar per a una auditoria forense instantània.

### 2. Immutabilitat i Versionat (Prompt SemVer)

Un prompt és codi. Ha d'estar controlat per versions. Qualsevol canvi en una instrucció interna, per petit que sigui, constitueix una nova versió immutable de l'agent (v1.0 -> v1.1). No existeixen canvis "en calent" en producció.

### 3. Validació Estricta a l'Entrada (Fail Fast)

Actuem com un control de duanes estricte. Abans que un agent comenci a treballar, el sistema verifica automàticament que les dades que rebrà compleixen exactament amb el seu contracte d'entrada. Si les dades no encaixen al 100%, el procés s'atura immediatament amb un error visible. Aquest patró de "Fail Fast" és essencial per a l'estabilitat de sistemes distribuïts [5].

### 4. Mínim Privilegi Contextual

La informació es regeix pel principi de "necessitat de saber". Cap agent rep el context global de l'operació, només les dades estrictament necessàries per a la seva microtasca. Això és crític, ja que s'ha demostrat que el rendiment dels LLMs es degrada significativament quan se'ls inunda amb context irrellevant ("Lost in the Middle phenomenon") [6].

### 5. Economia Unitària (FinOps at the Atomic Level)

El cost ha de ser observable per unitat. El sistema ha de ser capaç de reportar el cost exacte d'execució de cada microagent individual.


## 5. El Marc de Qualitat (Testing Framework)

Atès que els LLMs són probabilístics, el testing en MAS ha de ser estadístic i multinivell.

* **Nivell 1: Avaluacions Unitàries (Unit Evals).** Cada Microagent ha de superar un "Golden Dataset" amb un llindar d'èxit estadístic definit (>95%) abans de ser desplegat.
* **Nivell 2: Testing de Contracte (Integration).** Validem que les peces encaixin mitjançant Mocking. Assegurem que l'orquestrador està transformant correctament les dades entre agents sense necessitat d'executar els models.
* **Nivell 3: Testing de Procés (E2E).** Validem que el flux de negoci complet compleix amb els requisits funcionals i de latència.


## 6. Les Tres Dimensions de l'Escalabilitat

En el paradigma monolític, escalar és costós i fràgil. En MAS, l'escalabilitat és una conseqüència natural de l'arquitectura.

### I. Escalabilitat Tècnica: "Stateless per Disseny"

Els nostres microagents són unitats d'execució sense estat (stateless). Això permet desplegar des d'arquitectures simples fins a sistemes asíncrons basats en cues (Event-Driven) per gestionar pics de càrrega massius, sense necessitat de modificar la lògica interna dels agents.

### II. Escalabilitat Cognitiva: "Divideix i Venceràs"

Evitem el deteriorament cognitiu dels contextos llargs [6]. Per resoldre problemes més complexos, no ampliem el context; afegim més agents especialitzats a la cadena. Mantenim la fiabilitat constant independentment de la complexitat del problema.

### III. Escalabilitat Organitzacional: Desenvolupament Modular

Trenquem el coll d'ampolla del desenvolupament. Gràcies als contractes estrictes i caixes negres, múltiples equips poden treballar, optimitzar i desplegar diferents microagents en paral·lel sense conflictes de codi i sense aturar l'ecosistema.


## 7. Arquitectura de Referència: El Motor de Licitacions (RFP Engine)

Per demostrar la robustesa del Microagentic Stacking en un entorn crític, analitzem l'arquitectura lògica d'un sistema de Resposta Automàtica a Licitacions (RFPs). Aquest procés requereix una estricta separació entre el raonament (IA) i les dades de negoci (SQL). La indústria es mou cap a models on l'orquestració es gestiona mitjançant màquines d'estat explícites, no mitjançant bucles autònoms [9].

### La Pila Microagèntica (The Stack)

* **Orquestrador (State Machine):** El nucli del sistema. No és IA. És un motor de flux de treball que gestiona l'estat de la licitació i dirigeix el trànsit entre agents i bases de dades.
* **Microagent A (Extractor):** Rep text cru del PDF. La seva única missió és retornar un JSON estructurat de requisits tècnics. No opina, només extreu.
* **Capa d'Integració (Legacy):** L'Orquestrador pren els IDs extrets per l'Agent A i consulta l'ERP per obtenir preus i estoc. Principi Clau: La IA mai inventa preus.
* **Microagent B (Auditor de Risc):** Rep les clàusules legals. Si detecta riscos inacceptables, activa un "Tallacircuits" (Circuit Breaker) [5] i l'orquestrador atura el procés abans de la redacció.
* **Microagent C (Redactor Final):** Només s'activa si els passos anteriors són vàlids. Genera la proposta utilitzant exclusivament les "dades netes" que l'orquestrador li proporciona.


## 8. Conclusió: L'Evolució com a Estàndard

Microagentic Stacking no és una solució estàtica; és una metodologia per al creixement continu. Permet començar amb un MVP simple i evolucionar cap a ecosistemes complexos, afegint capacitats i optimitzant components individuals sense risc de regressió. La comunitat de desenvolupament en general està adoptant aquesta transició des de monòlits cap a fluxos de treball agèntics com el nou paradigma de migració de càrregues de treball [12].

Rebutgem el caos. Abracem l'estructura.
**No construïm demos. Construïm arquitectura.**

**Autor Principal & Mantenidor:** Eric Mora Juan (<ericmora82@gmail.com>)
**Publicat:** Gener 2026
Aquest és un estàndard viu. Les contribucions de la comunitat són benvingudes.


## Referències

### Fonaments d'Enginyeria de Software

1. Newman, S. (2021). Building Microservices: Designing Fine-Grained Systems (2nd Ed.). O'Reilly Media.
2. Martin, R. C. (2017). Clean Architecture: A Craftsman's Guide to Software Structure and Design. Prentice Hall.
3. Meyer, B. (1992). "Applying 'Design by Contract'". Computer, 25(10), 40-51. IEEE. Link: [https://ieeexplore.ieee.org/document/161279](https://ieeexplore.ieee.org/document/161279)
4. Hohpe, G., & Woolf, B. (2003). Enterprise Integration Patterns: Designing, Building, and Deploying Messaging Solutions. Addison-Wesley.
5. Nygard, M. T. (2018). Release It!: Design and Deploy Production-Ready Software (2nd Ed.). Pragmatic Bookshelf.

### Investigació i Arquitectura de Sistemes d'IA (Estat de l'Art)

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

### Consens Industrial Recent (2025)

1. Forrester Research (2025). "The Agentic AI Reality Check: Why Governance and Orchestration Will Define the Next Era of Enterprise Automation." (Informe de Tendències Tecnològiques).
