# THE MICROAGENTIC STACKING MANIFESTO

> Note : Cette traduction a été réalisée automatiquement par Gemini 3.

## De l'Alchimie des Prompts à l'Ingénierie Logicielle Évolutive

## 1. Préambule : La Fin du Monolithe

Nous assistons à l'effondrement du "Prompt Engineering" en tant que discipline isolée. La tentative de résoudre des processus d'affaires complexes via une instruction unique géante à un modèle fondationnel (LLM) s'est avérée être une stratégie fragile, imprévisible et impossible à auditer à l'échelle de l'entreprise.

La recherche académique confirmait déjà en 2023 que traiter les LLMs comme des boîtes noires monolithiques pour des tâches complexes était une impasse [7]. Aujourd'hui, des institutions leaders comme UC Berkeley ratifient que l'état de l'art n'est plus atteint avec des modèles individuels plus grands, mais avec des "Systèmes d'IA Composés" qui orchestrent de multiples composants [13], une tendance validée par les modèles d'architecture émergents observés dans l'industrie par des firmes leaders comme a16z [15].

L'IA n'est pas magique ; c'est du calcul probabiliste. En tant que tel, elle doit être soumise aux mêmes disciplines d'ingénierie qui ont permis aux logiciels de passer à l'échelle pendant des décennies : découplage, modularité et contrats stricts. L'avenir de l'IA ne réside pas dans des prompts plus grands, mais dans une meilleure architecture des systèmes [10].

Nous proposons un changement de paradigme radical : cesser de construire des chatbots monolithiques et commencer à orchestrer des architectures composées.

Nous appelons ce standard **Microagentic Stacking (MAS)**.

## 2. Philosophie Centrale

Notre méthodologie ne cherche pas à créer une Intelligence Artificielle Générale (AGI). Elle cherche à construire des systèmes d'entreprise robustes via l'orchestration d'unités cognitives spécialisées.

Nous nous basons sur trois piliers non négociables :

1. **Le Processus Prime :** L'IA ne définit pas le flux de travail ; le processus métier définit où et comment l'IA est utilisée.
2. **Atomicité sur Généralité :** La complexité cognitive est résolue en la divisant en ses plus petits composants indivisibles.
3. **Croissance Incrémentale :** Les systèmes ne sont pas conçus "finis" ; ils évoluent couche par couche, processus par processus, d'un MVP simple à un écosystème complexe.

## 3. Les Principes Techniques du MAS

Pour implémenter un système MAS, il faut obéir aux lois d'architecture suivantes, héritées de décennies de principes solides d'ingénierie logicielle :

### I. La Loi du Microagent Atomique (Single Responsibility)

Un Microagent doit exécuter une seule tâche cognitive et l'exécuter parfaitement. C'est l'application directe du Principe de Responsabilité Unique (SRP) aux composants d'IA [2]. Si un agent tente de "chercher des informations, les analyser et rédiger une réponse", il est mal conçu. Il doit être divisé en trois agents distincts.

### II. L'Isolation de Boîte Noire (The Black Box Principle)

Le fonctionnement interne d'un Microagent est absolument privé et inaccessible au reste du système, suivant les principes de conception de microservices et les contextes délimités [1].

* L'orchestrateur ne sait pas quel prompt est utilisé en interne.
* L'orchestrateur ne sait pas quel modèle (GPT-4, Claude, Llama 3 local) exécute la tâche.

Cette abstraction permet de refactoriser, d'optimiser les coûts et de changer de modèle au sein d'un agent sans casser le processus supérieur.

### III. Découplage Radical et Contrats (Decoupling via Schema)

Les Microagents sont agnostiques entre eux. Ils sont régis par la méthodologie de "Conception par Contrat", où les préconditions et postconditions sont strictes [3].

* **Contrats Rigides :** Chaque agent définit strictement quelles données il accepte (Input Schema) et quelles données il renvoie (Output Schema) en utilisant des formats standard (par ex., JSON Schema, Pydantic).
* **L'Orchestrateur comme Transformateur :** Il est de la responsabilité exclusive du Processus Métier (l'orchestrateur) de prendre la sortie de l'Agent A, transformer ou mapper les données si nécessaire, et les injecter dans l'Agent B en respectant son contrat.

### IV. Orchestration Hiérarchique et Composable

Les agents sont les pièces, mais la valeur est dans l'assemblage. L'intelligence complexe n'émerge pas d'un seul modèle, mais de la coordination de multiples parties [4].

* **Processus appelant des Agents :** Un flux de travail orchestre une séquence de microagents.
* **Processus appelant des Processus :** Un processus de haut niveau peut invoquer un autre processus comme s'il s'agissait d'un simple agent, permettant une composition récursive infinie.

## 4. L'Accord de Gouvernance d'Entreprise

L'autonomie de l'IA au sein d'une entreprise nécessite un contrôle strict. MAS n'est pas juste du code ; c'est un cadre de responsabilité et de robustesse. Des experts en ingénierie de ML ont souligné à plusieurs reprises que le fossé entre une démo et un système en production réside dans le manque de rigueur d'ingénierie, d'évaluation et de contrôle des risques [14]. Les preuves montrent que la robustesse diminue considérablement à mesure que l'autonomie incontrôlée augmente [8].

### 1. Traçabilité Atomique (Atomic Accountability)

L'erreur "système" n'existe pas. Chaque output généré doit porter une signature de trace immuable identifiant quel microagent spécifique, quelle version du prompt et quel modèle exact l'a généré pour un audit judiciaire instantané.

### 2. Immutabilité et Versionning (Prompt SemVer)

Un prompt est du code. Il doit être sous contrôle de version. Tout changement dans une instruction interne, aussi minime soit-il, constitue une nouvelle version immuable de l'agent (par ex., v1.0.0 pour des ajustements mineurs du texte, v2.0.0 pour un changement de modèle ou de logique). Il n'y a pas de changements "à chaud" en production.

### 3. Validation Stricte à l'Entrée (Fail Fast)

Nous agissons comme un contrôle douanier strict. Avant qu'un agent ne commence à travailler, le système vérifie automatiquement que les données qu'il va recevoir sont exactement conformes à son contrat d'entrée. Si les données ne correspondent pas à 100%, le processus s'arrête immédiatement avec une erreur visible. Ce modèle de "Fail Fast" est essentiel pour la stabilité des systèmes distribués [5].

### 4. Privilège Contextuel Minimum

L'information est régie par le principe du "besoin de savoir". Aucun agent ne reçoit le contexte global de l'opération, seulement les données strictement nécessaires à sa micro-tâche. Ceci est critique, car il a été démontré que la performance des LLMs se dégrade considérablement lorsqu'ils sont inondés de contexte non pertinent ("Lost in the Middle phenomenon") [6].

### 5. Économie Unitaire (FinOps at the Atomic Level)

Le coût doit être observable par unité. Le système doit être capable de rapporter le coût exact d'exécution de chaque microagent individuel.

## 5. Le Cadre de Qualité (Testing Framework)

Comme les LLMs sont probabilistes, les tests en MAS doivent être statistiques et multiniveaux.

* **Niveau 1 : Évaluations Unitaires (Unit Evals).** Chaque Microagent doit réussir un "Golden Dataset" avec un seuil de succès statistique défini (>95%) avant d'être déployé.
* **Niveau 2 : Test de Contrat (Integration).** Nous validons que les pièces s'emboîtent via le Mocking. Nous assurons que l'orchestrateur transforme correctement les données entre agents sans avoir besoin d'exécuter les modèles.
* **Niveau 3 : Test de Processus (E2E).** Nous validons que le flux métier complet répond aux exigences fonctionnelles et de latence.

## 6. Les Trois Dimensions de l'Évolutivité

Dans le paradigme monolithique, la mise à l'échelle est coûteuse et fragile. En MAS, l'évolutivité est une conséquence naturelle de l'architecture.

### I. Évolutivité Technique : "Stateless by Design"

Nos microagents sont des unités d'exécution sans état (stateless). Cela permet de déployer depuis des architectures simples jusqu'à des systèmes asynchrones basés sur des files d'attente (Event-Driven) pour gérer des pics de charge massifs, sans avoir besoin de modifier la logique interne des agents.

### II. Évolutivité Cognitive : "Diviser pour Régner"

Nous évitons la détérioration cognitive des contextes longs [6]. Pour résoudre des problèmes plus complexes, nous n'agrandissons pas le contexte ; nous ajoutons plus d'agents spécialisés à la chaîne. Nous maintenons la fiabilité constante indépendamment de la complexité du problème.

### III. Évolutivité Organisationnelle : Développement Modulaire

Nous brisons le goulot d'étranglement du développement. Grâce aux contrats stricts et aux boîtes noires, plusieurs équipes peuvent travailler, optimiser et déployer différents microagents en parallèle sans conflits de code et sans arrêter l'écosystème.

## 7. Architecture de Référence : Le Moteur d'Appels d'Offres (RFP Engine)

Pour démontrer la robustesse du Microagentic Stacking dans un environnement critique, nous analysons l'architecture logique d'un système de Réponse Automatique aux Appels d'Offres (RFP). Ce processus nécessite une séparation stricte entre le raisonnement (IA) et les données métier (SQL). L'industrie s'oriente vers des modèles où l'orchestration est gérée par des machines d'état explicites, et non par des boucles autonomes [9].

### La Pile Microagentique (The Stack)

* **Orchestrateur (State Machine) :** Le cœur du système. Ce n'est pas de l'IA. C'est un moteur de workflow qui gère l'état de l'appel d'offres et dirige le trafic entre les agents et les bases de données.
* **Microagent A (Extracteur) :** Reçoit le texte brut du PDF. Sa seule mission est de renvoyer un JSON structuré des exigences techniques. Il ne donne pas d'opinion, il extrait seulement.
* **Couche d'Intégration (Legacy) :** L'Orchestrateur prend les IDs extraits par l'Agent A et interroge l'ERP pour obtenir prix et stock. Principe Clé : L'IA n'invente jamais de prix.
* **Microagent B (Auditeur de Risque) :** Reçoit les clauses légales. S'il détecte des risques inacceptables, il active un "Coupe-Circuit" (Circuit Breaker) [5] et l'orchestrateur arrête le processus avant la rédaction.
* **Microagent C (Rédacteur Final) :** Ne s'active que si les étapes précédentes sont valides. Génère la proposition en utilisant exclusivement les "données propres" que l'orchestrateur lui fournit.

## 8. Conclusion : L'Évolution comme Standard

Microagentic Stacking n'est pas une solution statique ; c'est une méthodologie pour la croissance continue. Elle permet de commencer avec un MVP simple et d'évoluer vers des écosystèmes complexes, en ajoutant des capacités et en optimisant des composants individuels sans risque de régression. La communauté de développement en général adopte cette transition des monolithes vers des workflows agentiques comme le nouveau paradigme de migration des charges de travail [12].

Nous rejetons le chaos. Nous embrassons la structure.
**Nous ne construisons pas des démos. Nous construisons une architecture.**

**Auteur Principal & Mainteneur :** Eric Mora Juan (<ericmora82@gmail.com>)
**Publié :** Janvier 2026
Ceci est un standard vivant. Les contributions de la communauté sont les bienvenues.
Adoptez cette norme en ajoutant le badge MAS-Ready à votre dépôt.

## Références

### Fondamentaux du Génie Logiciel

1. Newman, S. (2021). Building Microservices: Designing Fine-Grained Systems (2nd Ed.). O'Reilly Media.
2. Martin, R. C. (2017). Clean Architecture: A Craftsman's Guide to Software Structure and Design. Prentice Hall.
3. Meyer, B. (1992). "Applying 'Design by Contract'". Computer, 25(10), 40-51. IEEE. Link: [https://ieeexplore.ieee.org/document/161279](https://ieeexplore.ieee.org/document/161279)
4. Hohpe, G., & Woolf, B. (2003). Enterprise Integration Patterns: Designing, Building, and Deploying Messaging Solutions. Addison-Wesley.
5. Nygard, M. T. (2018). Release It!: Design and Deploy Production-Ready Software (2nd Ed.). Pragmatic Bookshelf.

### Recherche et Architecture des Systèmes d'IA (État de l'Art)

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

### Consensus Industriel Récent (2025)

1. Forrester Research (2025). "The Agentic AI Reality Check: Why Governance and Orchestration Will Define the Next Era of Enterprise Automation." (Rapport des Tendances Technologiques).
