# THE MICROAGENTIC STACKING MANIFESTO

> Nota: Esta traducción ha sido realizada automáticamente por Gemini 3.

## De la Alquimia de los Prompts a la Ingeniería de Software Escalable

## 1. Preámbulo: El Fin del Monolito

Estamos presenciando el colapso del "Prompt Engineering" como disciplina aislada. El intento de resolver procesos de negocio complejos mediante una única instrucción gigante a un modelo fundacional (LLM) ha demostrado ser una estrategia frágil, impredecible e imposible de auditar a escala empresarial.

La investigación académica ya confirmaba en 2023 que tratar a los LLMs como cajas negras monolíticas para tareas complejas era un callejón sin salida [7]. Hoy, instituciones líderes como UC Berkeley ratifican que el estado del arte ya no se logra con modelos individuales más grandes, sino con "Sistemas Compuestos de IA" que orquestan múltiples componentes [13], una tendencia validada por los patrones de arquitectura emergentes observados en la industria por firmas líderes como a16z [15].

La IA no es magia; es cómputo probabilístico. Como tal, debe someterse a las mismas disciplinas de ingeniería que han permitido escalar el software durante décadas: desacoplamiento, modularidad y contratos estrictos. El futuro de la IA no está en prompts más grandes, sino en una mejor arquitectura de sistemas [10].

Proponemos un cambio de paradigma radical: dejar de construir chatbots monolíticos y empezar a orquestar arquitecturas compuestas.

A este estándar lo llamamos **Microagentic Stacking (MAS)**.

## 2. Filosofía Central

Nuestra metodología no busca crear una Inteligencia Artificial General (AGI). Busca construir sistemas empresariales robustos mediante la orquestación de unidades cognitivas especializadas.

Nos basamos en tres pilares innegociables:

1. **El Proceso Manda:** La IA no define el flujo de trabajo; el proceso de negocio define dónde y cómo se utiliza la IA.
2. **Atomicidad sobre Generalidad:** La complejidad cognitiva se resuelve dividiéndola en sus componentes más pequeños e indivisibles.
3. **Crecimiento Incremental:** Los sistemas no se diseñan "finalizados"; evolucionan capa a capa, proceso a proceso, desde un MVP simple hasta un ecosistema complejo.

## 3. Los Principios Técnicos del MAS

Para implementar un sistema MAS, se deben obedecer las siguientes leyes de arquitectura, heredadas de décadas de principios sólidos de ingeniería de software:

### I. La Ley del Microagente Atómico (Single Responsibility)

Un Microagente debe ejecutar una sola tarea cognitiva y ejecutarla perfectamente. Esta es la aplicación directa del Principio de Responsabilidad Única (SRP) a los componentes de IA [2]. Si un agente intenta "buscar información, analizarla y redactar una respuesta", está mal diseñado. Debe dividirse en tres agentes distintos.

### II. El Aislamiento de Caja Negra (The Black Box Principle)

El funcionamiento interno de un Microagente es absolutamente privado e inaccesible para el resto del sistema, siguiendo los principios de diseño de microservicios y contextos delimitados [1].

* El orquestador no sabe qué prompt se utiliza internamente.
* El orquestador no sabe qué modelo (GPT-4, Claude, Llama 3 local) ejecuta la tarea.

Esta abstracción permite refactorizar, optimizar costes y cambiar modelos dentro de un agente sin romper el proceso superior.

### III. Desacoplamiento Radical y Contratos (Decoupling via Schema)

Los Microagentes son agnósticos entre sí. Se rigen por la metodología de "Diseño por Contrato", donde las precondiciones y postcondiciones son estrictas [3].

* **Contratos Rígidos:** Cada agente define estrictamente qué datos acepta (Input Schema) y qué datos devuelve (Output Schema) usando formatos estándar (p. ej., JSON Schema, Pydantic).
* **El Orquestador como Transformador:** Es responsabilidad exclusiva del Proceso de Negocio (el orquestador) tomar la salida del Agente A, transformar o mapear los datos si es necesario, e inyectarlos en el Agente B cumpliendo su contrato.

### IV. Orquestación Jerárquica y Composable

Los agentes son las piezas, pero el valor está en el ensamblaje. La inteligencia compleja no emerge de un solo modelo, sino de la coordinación de múltiples partes [4].

* **Procesos que llaman a Agentes:** Un flujo de trabajo orquesta una secuencia de microagentes.
* **Procesos que llaman a Procesos:** Un proceso de alto nivel puede invocar a otro proceso como si fuera un agente más, permitiendo una composición recursiva infinita.

## 4. El Acuerdo de Gobernanza Empresarial

La autonomía de la IA dentro de una empresa requiere un control estricto. MAS no es solo código; es un marco de responsabilidad y robustez. Expertos en ingeniería de ML han señalado reiteradamente que la brecha entre una demo y un sistema en producción reside en la falta de rigor de ingeniería, evaluación y control de riesgos [14]. La evidencia muestra que la robustez disminuye drásticamente a medida que aumenta la autonomía no controlada [8].

### 1. Trazabilidad Atómica (Atomic Accountability)

El error "del sistema" no existe. Cada output generado debe llevar una firma de traza inmutable que identifique qué microagente específico, qué versión del prompt y qué modelo exacto lo generó para una auditoría forense instantánea.

### 2. Inmutabilidad y Versionado (Prompt SemVer)

Un prompt es código. Debe estar bajo control de versiones. Cualquier cambio en una instrucción interna, por pequeño que sea, constituye una nueva versión inmutable del agente (p. ej., v1.0.0 para ajustes menores de texto, v2.0.0 para cambio de modelo o lógica). No existen cambios "en caliente" en producción.

### 3. Validación Estricta en la Entrada (Fail Fast)

Actuamos como un control de aduanas estricto. Antes de que un agente empiece a trabajar, el sistema verifica automáticamente que los datos que va a recibir cumplen exactamente con su contrato de entrada. Si los datos no encajan al 100%, el proceso se detiene inmediatamente con un error visible. Este patrón de "Fail Fast" es esencial para la estabilidad de sistemas distribuidos [5].

### 4. Mínimo Privilegio Contextual

La información se rige por el principio de "necesidad de saber". Ningún agente recibe el contexto global de la operación, solo los datos estrictamente necesarios para su micro-tarea. Esto es crítico, ya que se ha demostrado que el rendimiento de los LLMs se degrada significativamente cuando se les inunda con contexto irrelevante ("Lost in the Middle phenomenon") [6].

### 5. Economía Unitaria (FinOps at the Atomic Level)

El coste debe ser observable por unidad. El sistema debe ser capaz de reportar el coste exacto de ejecución de cada microagente individual.

## 5. El Marco de Calidad (Testing Framework)

Dado que los LLMs son probabilísticos, el testing en MAS debe ser estadístico y multinivel.

* **Nivel 1: Evaluaciones Unitarias (Unit Evals).** Cada Microagente debe superar un "Golden Dataset" con un umbral de éxito estadístico definido (>95%) antes de ser desplegado.
* **Nivel 2: Testing de Contrato (Integration).** Validamos que las piezas encajen mediante Mocking. Aseguramos que el orquestador está transformando correctamente los datos entre agentes sin necesidad de ejecutar los modelos.
* **Nivel 3: Testing de Proceso (E2E).** Validamos que el flujo de negocio completo cumple con los requisitos funcionales y de latencia.

## 6. Las Tres Dimensiones de la Escalabilidad

En el paradigma monolítico, escalar es costoso y frágil. En MAS, la escalabilidad es una consecuencia natural de la arquitectura.

### I. Escalabilidad Técnica: "Stateless por Diseño"

Nuestros microagentes son unidades de ejecución sin estado (stateless). Esto permite desplegar desde arquitecturas simples hasta sistemas asíncronos basados en colas (Event-Driven) para gestionar picos de carga masivos, sin necesidad de modificar la lógica interna de los agentes.

### II. Escalabilidad Cognitiva: "Divide y Vencerás"

Evitamos el deterioro cognitivo de los contextos largos [6]. Para resolver problemas más complejos, no ampliamos el contexto; agregamos más agentes especializados a la cadena. Mantenemos la fiabilidad constante independientemente de la complejidad del problema.

### III. Escalabilidad Organizacional: Desarrollo Modular

Rompemos el cuello de botella del desarrollo. Gracias a los contratos estrictos y cajas negras, múltiples equipos pueden trabajar, optimizar y desplegar diferentes microagentes en paralelo sin conflictos de código y sin detener el ecosistema.

## 7. Arquitectura de Referencia: El Motor de Licitaciones (RFP Engine)

Para demostrar la robustez del Microagentic Stacking en un entorno crítico, analizamos la arquitectura lógica de un sistema de Respuesta Automática a Licitaciones (RFPs). Este proceso requiere una estricta separación entre el razonamiento (IA) y los datos de negocio (SQL). La industria se mueve hacia modelos donde la orquestación se gestiona mediante máquinas de estado explícitas, no mediante bucles autónomos [9].

### La Pila Microagéntica (The Stack)

* **Orquestador (State Machine):** El núcleo del sistema. No es IA. Es un motor de flujo de trabajo que gestiona el estado de la licitación y dirige el tráfico entre agentes y bases de datos.
* **Microagente A (Extractor):** Recibe texto crudo del PDF. Su única misión es devolver un JSON estructurado de requisitos técnicos. No opina, solo extrae.
* **Capa de Integración (Legacy):** El Orquestador toma los IDs extraídos por el Agente A y consulta el ERP para obtener precios y stock. Principio Clave: La IA nunca inventa precios.
* **Microagente B (Auditor de Riesgo):** Recibe las cláusulas legales. Si detecta riesgos inaceptables, activa un "Cortocircuito" (Circuit Breaker) [5] y el orquestador detiene el proceso antes de la redacción.
* **Microagente C (Redactor Final):** Solo se activa si los pasos anteriores son válidos. Genera la propuesta utilizando exclusivamente los "datos limpios" que el orquestador le proporciona.

## 8. Conclusión: La Evolución como Estándar

Microagentic Stacking no es una solución estática; es una metodología para el crecimiento continuo. Permite empezar con un MVP simple y evolucionar hacia ecosistemas complejos, añadiendo capacidades y optimizando componentes individuales sin riesgo de regresión. La comunidad de desarrollo en general está adoptando esta transición desde monolitos hacia flujos de trabajo agénticos como el nuevo paradigma de migración de cargas de trabajo [12].

Rechazamos el caos. Abrazamos la estructura.
**No construimos demos. Construimos arquitectura.**

**Autor Principal & Mantenedor:** Eric Mora Juan (<ericmora82@gmail.com>)
**Publicado:** Enero 2026
Este es un estándar vivo. Las contribuciones de la comunidad son bienvenidas.
Adopta este estándar añadiendo la insignia MAS-Ready a tu repositorio.

## Referencias

### Fundamentos de Ingeniería de Software

1. Newman, S. (2021). Building Microservices: Designing Fine-Grained Systems (2nd Ed.). O'Reilly Media.
2. Martin, R. C. (2017). Clean Architecture: A Craftsman's Guide to Software Structure and Design. Prentice Hall.
3. Meyer, B. (1992). "Applying 'Design by Contract'". Computer, 25(10), 40-51. IEEE. Link: [https://ieeexplore.ieee.org/document/161279](https://ieeexplore.ieee.org/document/161279)
4. Hohpe, G., & Woolf, B. (2003). Enterprise Integration Patterns: Designing, Building, and Deploying Messaging Solutions. Addison-Wesley.
5. Nygard, M. T. (2018). Release It!: Design and Deploy Production-Ready Software (2nd Ed.). Pragmatic Bookshelf.

### Investigación y Arquitectura de Sistemas de IA (Estado del Arte)

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

### Consenso Industrial Reciente (2025)

1. Forrester Research (2025). "The Agentic AI Reality Check: Why Governance and Orchestration Will Define the Next Era of Enterprise Automation." (Informe de Tendencias Tecnológicas).
