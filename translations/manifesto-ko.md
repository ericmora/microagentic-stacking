# 마이크로에이전트 스태킹 선언문 (THE MICROAGENTIC STACKING MANIFESTO)

> 참고: 이 번역은 Gemini 3에 의해 자동 생성되었습니다.

## 프롬프트 연금술에서 확장 가능한 소프트웨어 엔지니어링으로

---

## 1. 서문: 모놀리스의 종말

우리는 고립된 규율로서의 "프롬프트 엔지니어링"의 붕괴를 목격하고 있습니다. 단일 거대 명령어를 파운데이션 모델(LLM)에 전달하여 복잡한 비즈니스 프로세스를 해결하려는 시도는 깨지기 쉽고 예측 불가능한 전략이며, 엔터프라이즈 규모에서 감사가 불가능하다는 것이 입증되었습니다.

학계 연구는 이미 2023년에 LLM을 복잡한 작업을 위한 모놀리식 블랙박스로 취급하는 것이 막다른 골목임을 확인했습니다 [7]. 오늘날, UC 버클리와 같은 선도 기관들은 최첨단 기술이 더 이상 더 큰 개별 모델로 달성되는 것이 아니라 여러 구성 요소를 조정하는 "복합 AI 시스템(Compound AI Systems)"으로 달성된다는 것을 비준하고 있으며 [13], 이는 a16z와 같은 주요 기업이 업계에서 관찰한 새로운 아키텍처 패턴에 의해 검증된 추세입니다 [15].

AI는 마술이 아닙니다. 확률론적 계산입니다. 따라서 소프트웨어가 수십 년 동안 확장될 수 있었던 것과 동일한 엔지니어링 규율, 즉 분리, 모듈성 및 엄격한 계약을 거쳐야 합니다. AI의 미래는 더 나은 프롬프트가 아니라 더 나은 시스템 아키텍처에 있습니다 [10].

우리는 급진적인 패러다임 전환을 제안합니다. 모놀리식 챗봇 구축을 중단하고 복합 아키텍처 조정을 시작하십시오.

우리는 이 표준을 **마이크로에이전트 스태킹(Microagentic Stacking, MAS)**이라고 부릅니다.

---

## 2. 핵심 철학

우리의 방법론은 인공 일반 지능(AGI)을 창조하려는 것이 아닙니다. 전문화된 인지 단위의 조정을 통해 강력한 엔터프라이즈 시스템을 구축하려는 것입니다.

우리는 협상할 수 없는 세 가지 기둥에 기반을 두고 있습니다.

1. **AI보다 프로세스 우선:** AI가 워크플로를 정의하지 않습니다. 비즈니스 프로세스가 AI의 사용 위치와 방법을 정의합니다.
2. **일반성보다 원자성:** 인지적 복잡성은 가장 작고 나눌 수 없는 구성 요소로 분해함으로써 해결됩니다.
3. **점진적 성장:** 시스템은 "완성된" 상태로 설계되지 않습니다. 단순한 MVP에서 복잡한 생태계로, 레이어별로, 프로세스별로 진화합니다.

---

## 3. MAS의 기술 원칙

MAS 시스템을 구현하려면 수십 년간의 건전한 소프트웨어 엔지니어링 원칙에서 계승된 다음 아키텍처 법칙을 준수해야 합니다.

### I. 원자적 마이크로에이전트의 법칙 (단일 책임)

마이크로에이전트는 단일 인지 작업을 수행하고 완벽하게 수행해야 합니다. 이것은 단일 책임 원칙(SRP)을 AI 구성 요소에 직접 적용한 것입니다 [2]. 에이전트가 "정보를 검색하고, 분석하고, 응답을 작성"하려고 하면 잘못 설계된 것입니다. 세 개의 별도 에이전트로 나누어야 합니다.

### II. 블랙박스 격리 (블랙박스 원칙)

마이크로에이전트의 내부 작동은 마이크로서비스 설계 원칙과 경계 컨텍스트에 따라 시스템의 나머지 부분에서 절대적으로 비공개이며 액세스할 수 없습니다 [1].

* 오케스트레이터는 내부적으로 어떤 프롬프트가 사용되는지 모릅니다.
* 오케스트레이터는 어떤 모델(GPT-4, Claude, 로컬 Llama 3)이 작업을 수행하는지 모릅니다.

이러한 추상화를 통해 상위 프로세스를 중단하지 않고 에이전트 내에서 리팩터링, 비용 최적화 및 모델 변경이 가능합니다.

### III. 급진적 분리 및 계약 (스키마를 통한 분리)

마이크로에이전트는 서로 불가지론적입니다. 그들은 "계약에 의한 설계" 방법론에 의해 관리되며, 여기서 전제 조건과 사후 조건은 엄격합니다 [3].

* **엄격한 계약 (Rigid Contracts):** 각 에이전트는 표준 형식(예: JSON Schema, Pydantic)을 사용하여 허용하는 데이터(Input Schema)와 반환하는 데이터(Output Schema)를 엄격하게 정의합니다.
* **변환기 건으로서의 오케스트레이터:** 에이전트 A의 출력을 가져와 필요한 경우 데이터를 변환하거나 매핑하고 계약을 충족하는 에이전트 B에 주입하는 것은 비즈니스 프로세스(오케스트레이터)의 배타적 책임입니다.

### IV. 계층적이고 구성 가능한 오케스트레이션

에이전트는 부품이지만 가치는 조립에 있습니다. 복잡한 지능은 단일 모델에서 나오는 것이 아니라 여러 부분의 조정에서 나옵니다 [4].

* **에이전트를 호출하는 프로세스:** 워크플로는 일련의 마이크로에이전트를 조정합니다.
* **프로세스를 호출하는 프로세스:** 고수준 프로세스는 다른 프로세스를 마치 또 다른 에이전트인 것처럼 호출하여 무한한 재귀적 구성을 허용할 수 있습니다.

---

## 4. 엔터프라이즈 거버넌스 계약

기업 내 AI 자율성에는 엄격한 통제가 필요합니다. MAS는 단순한 코드가 아닙니다. 책임과 견고성의 프레임워크입니다. ML 엔지니어링 전문가들은 데모와 프로덕션 시스템 간의 격차가 엔지니어링 엄격성, 평가 및 위험 통제의 부족에 있다고 반복해서 지적했습니다 [14]. 증거에 따르면 통제되지 않은 자율성이 증가함에 따라 견고성이 급격히 감소합니다 [8].

### 1. 원자적 책임 (Atomic Accountability)

"시스템 오류"는 존재하지 않습니다. 생성된 모든 출력은 즉각적인 포렌식 감사를 위해 어떤 특정 마이크로에이전트, 어떤 버전의 프롬프트, 어떤 정확한 모델이 생성했는지 식별하는 불변의 추적 서명 (immutable trace signature)을 포함해야 합니다.

### 2. 불변성 및 버전 관리 (Prompt SemVer)

프롬프트는 코드입니다. 버전 제어 하에 있어야 합니다. 내부 지침에 대한 변경은 아무리 사소하더라도 에이전트의 새로운 불변 버전(v1.0 -> v1.1)을 구성합니다. 프로덕션에서 "핫" 변경은 없습니다.

### 3. 엄격한 입력 검증 (Fail Fast)

우리는 엄격한 세관 통제 역할을 합니다. 에이전트가 작업을 시작하기 전에 시스템은 수신하려는 데이터가 입력 계약을 정확히 준수하는지 자동으로 확인합니다. 데이터가 100% 맞지 않으면 프로세스는 눈에 띄는 오류와 함께 즉시 중단됩니다. 이 "Fail Fast" 패턴은 분산 시스템 안정성에 필수적입니다 [5].

### 4. 최소 상황별 권한

정보는 "알 필요(need to know)" 원칙에 따라 관리됩니다. 어떤 에이전트도 작업의 글로벌 컨텍스트를 수신하지 않으며 해당 마이크로 작업에 엄격하게 필요한 데이터만 수신합니다. 관련 없는 컨텍스트로 넘쳐날 때 LLM 성능이 크게 저하되는 것으로 나타났기 때문에("Lost in the Middle 현상") 이는 매우 중요합니다 [6].

### 5. 단위 경제학 (원자 수준의 FinOps)

비용은 단위별로 관찰 가능해야 합니다. 시스템은 각 개별 마이크로에이전트의 정확한 실행 비용을 보고할 수 있어야 합니다.

---

## 5. 품질 프레임워크 (테스트 프레임워크)

LLM은 확률적이기 때문에 MAS의 테스트는 통계적이고 다단계적이어야 합니다.

* **레벨 1: 단위 평가 (Unit Evals).** 각 마이크로에이전트는 배포되기 전에 정의된 통계적 성공 임계값(>95%)이 있는 "골든 데이터세트"를 통과해야 합니다.
* **레벨 2: 계약 테스트 (통합).** 모킹을 사용하여 부품이 서로 맞는지 검증합니다. 모델을 실행할 필요 없이 오케스트레이터가 에이전트 간에 데이터를 올바르게 변환하고 있는지 확인합니다.
* **레벨 3: 프로세스 테스트 (E2E).** 전체 비즈니스 흐름이 기능 및 대기 시간 요구 사항을 충족하는지 검증합니다.

---

## 6. 확장성의 세 가지 차원

모놀리식 패러다임에서 확장은 비용이 많이 들고 깨지기 쉽습니다. MAS에서 확장성은 아키텍처의 자연스러운 결과입니다.

### I. 기술적 확장성: "설계에 의한 무상태"

우리의 마이크로에이전트는 무상태(stateless) 실행 단위입니다. 이를 통해 에이전트의 내부 로직을 수정할 필요 없이 단순한 아키텍처에서 대기열 기반 비동기 시스템(이벤트 기반)으로 배포하여 대규모 부하 스파이크를 관리할 수 있습니다.

### II. 인지적 확장성: "분할 정복"

우리는 긴 컨텍스트의 인지 저하를 피합니다 [6]. 더 복잡한 문제를 해결하기 위해 컨텍스트를 확장하지 않고 체인에 더 많은 전문 에이전트를 추가합니다. 문제의 복잡성에 관계없이 일관된 신뢰성을 유지합니다.

### III. 조직적 확장성: 모듈식 개발

우리는 개발 병목 현상을 해결합니다. 엄격한 계약과 블랙박스 덕분에 여러 팀이 코드 충돌 없이 생태계를 중단하지 않고 병렬로 다양한 마이크로에이전트를 작업, 최적화 및 배포할 수 있습니다.

---

## 7. 참조 아키텍처: RFP 엔진

중요한 환경에서 마이크로에이전트 스태킹의 견고성을 입증하기 위해 자동 제안 요청(RFP) 응답 시스템의 논리적 아키텍처를 분석합니다. 이 프로세스에는 추론(AI)과 비즈니스 데이터(SQL) 간의 엄격한 분리가 필요합니다. 업계는 오케스트레이션이 자율 루프가 아닌 명시적 상태 머신에 의해 관리되는 모델로 이동하고 있습니다 [9].

### 마이크로에이전트 스택

* **오케스트레이터(상태 머신):** 시스템의 핵심입니다. AI가 아닙니다. 입찰 상태를 관리하고 에이전트와 데이터베이스 간의 트래픽을 지시하는 워크플로 엔진입니다.
* **마이크로에이전트 A(추출기):** PDF에서 원시 텍스트를 받습니다. 유일한 임무는 기술 요구 사항의 구조화된 JSON을 반환하는 것입니다. 의견을 제시하지 않고 추출만 합니다.
* **통합 계층(레거시):** 오케스트레이터는 에이전트 A가 추출한 ID를 가져와 ERP를 조회하여 가격과 재고를 얻습니다. 핵심 원칙: AI는 가격을 발명하지 않습니다.
* **마이크로에이전트 B(위험 감사자):** 법적 조항을 받습니다. 용납할 수 없는 위험을 감지하면 "회로 차단기"[5]를 활성화하고 오케스트레이터는 초안 작성 전에 프로세스를 중단합니다.
* **마이크로에이전트 C(최종 초안 작성자):** 이전 단계가 유효한 경우에만 활성화됩니다. 오케스트레이터가 제공하는 "깨끗한 데이터"만을 사용하여 제안서를 생성합니다.

---

## 8. 결론: 표준으로서의 진화

마이크로에이전트 스태킹은 정적인 솔루션이 아닙니다. 지속적인 성장을 위한 방법론입니다. 단순한 MVP로 시작하여 복잡한 생태계로 진화하고 회귀 위험 없이 기능을 추가하고 개별 구성 요소를 최적화할 수 있습니다. 개발 커뮤니티 전반이 모놀리스에서 에이전트 워크플로 로의 전환을 워크로드 마이그레이션의 새로운 패러다임으로 채택하고 있습니다 [12].

우리는 혼란을 거부합니다. 우리는 구조를 수용합니다.
**우리는 데모를 만들지 않습니다. 우리는 아키텍처를 만듭니다.**

**주 저자 & 관리자:** Eric Mora Juan (<ericmora82@gmail.com>)
**게시:** 2026년 1월
이것은 살아있는 표준입니다. 커뮤니티 기여를 환영합니다.

---

## 참고 문헌

### 소프트웨어 엔지니어링 기초

1. Newman, S. (2021). Building Microservices: Designing Fine-Grained Systems (2nd Ed.). O'Reilly Media.
2. Martin, R. C. (2017). Clean Architecture: A Craftsman's Guide to Software Structure and Design. Prentice Hall.
3. Meyer, B. (1992). "Applying 'Design by Contract'". Computer, 25(10), 40-51. IEEE. Link: [https://ieeexplore.ieee.org/document/161279](https://ieeexplore.ieee.org/document/161279)
4. Hohpe, G., & Woolf, B. (2003). Enterprise Integration Patterns: Designing, Building, and Deploying Messaging Solutions. Addison-Wesley.
5. Nygard, M. T. (2018). Release It!: Design and Deploy Production-Ready Software (2nd Ed.). Pragmatic Bookshelf.

### AI 시스템 연구 및 아키텍처 (최첨단)

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

### 최근 업계 합의 (2025)

1. Forrester Research (2025). "The Agentic AI Reality Check: Why Governance and Orchestration Will Define the Next Era of Enterprise Automation." (Tech Trends Report).
