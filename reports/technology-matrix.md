# Technology Matrix

**Updated:** 2026-11-09
**Meaning:** This matrix records intended coverage. It is not evidence that a technology has been implemented. Verified status is recorded in `implementation-tracker.md` and project quality reports.

## Coverage by project

| # | Project | Backend | Frontend | Data and messaging | AI | Platform and operations |
|---:|---|---|---|---|---|---|
| 01 | Enterprise AI Knowledge Assistant | Python, FastAPI | React, TypeScript | PostgreSQL, pgvector | RAG, embeddings, hybrid search, LLM adapters, evaluation | Docker, GitHub Actions, OpenTelemetry |
| 02 | Multi-Agent AI Orchestration | Python, FastAPI, LangGraph | React, TypeScript | Redis, PostgreSQL | Agents, planning, tools, memory, approvals | Docker, tracing, replay |
| 03 | MCP Tool Ecosystem | Python, Node.js, TypeScript | Minimal client UI | PostgreSQL where needed | MCP resources, prompts, tools | OAuth, audit logging, containers |
| 04 | Developer Intelligence Copilot | Python, FastAPI | React, TypeScript | PostgreSQL, job queue | Code retrieval, LLM analysis, tool calling | GitHub App, webhooks, tracing |
| 05 | Enterprise Java Microservices | Java 21, Spring Boot, Spring Security | Minimal operations UI | PostgreSQL, Redis, Kafka | Optional operational insights only | Docker, resilience, OpenTelemetry |
| 06 | Customer Support Intelligence | Java, Spring Boot, Python | Angular, TypeScript, RxJS | PostgreSQL, Redis | RAG, classification, sentiment, summarization | Docker, tracing, metrics |
| 07 | Real-Time Analytics | Java, Python | React, TypeScript | Kafka, PostgreSQL, Redis | Anomaly detection, generated insights | Docker, WebSocket/SSE, observability |
| 08 | Career Intelligence | Python, FastAPI | Angular, TypeScript | PostgreSQL | Parsing, matching, RAG, interview evaluation | Docker, CI, privacy controls |
| 09 | Financial Insights | Java, Spring Boot, Python | React, TypeScript | PostgreSQL | Categorization, forecasting, explanations | Docker, CI, synthetic data |
| 10 | API Management | Java, Spring Boot | Angular, TypeScript | PostgreSQL, Redis, Kong | Optional API documentation assistant | Docker, OAuth2/JWT, analytics |
| 11 | LLM Observability | Python, FastAPI | React, TypeScript | PostgreSQL, Prometheus | Prompt and RAG evaluation, model comparison | OpenTelemetry, Grafana, Docker |
| 12 | Cloud Delivery Platform | Application-neutral | Application-neutral | Managed service integration | None required | Docker, Kubernetes, Helm, Terraform, AWS, GitHub Actions |
| 13 | Intelligent Commerce | Java, Spring Boot | React, TypeScript | Kafka, MongoDB, Redis, PostgreSQL where justified | Recommendations | Docker, tracing, sandbox payments |
| 14 | Document Automation | Python, FastAPI | React, TypeScript | PostgreSQL, object storage | OCR, classification, extraction, RAG | Workers, Docker, observability |
| 15 | Engineering Command Center | Java, Spring Boot, Python | Angular, TypeScript | PostgreSQL, Redis | LangGraph, MCP, engineering reports | Docker, Kubernetes, centralized telemetry |

## Capability allocation

### AI engineering

| Capability | Primary evidence projects |
|---|---|
| LLM provider integration | 01, 04, 06, 08, 11, 14, 15 |
| Retrieval-Augmented Generation | 01, 06, 08, 14 |
| Embeddings and semantic search | 01, 04, 06, 14 |
| Hybrid retrieval and reranking | 01, 04 |
| Agentic workflows | 02, 15 |
| Multi-agent architecture | 02, 15 |
| MCP | 03, 15 |
| Tool/function calling | 02, 03, 04, 15 |
| Prompt and context engineering | 01, 02, 04, 06, 08, 11, 14 |
| AI evaluation | 01, 06, 08, 11, 14 |
| AI observability | 02, 04, 11, 15 |
| AI application security | 01, 02, 03, 04, 06, 14, 15 |

### Backend engineering

| Capability | Primary evidence projects |
|---|---|
| Java 21 and Spring Boot | 05, 06, 07, 09, 10, 13, 15 |
| Python and FastAPI | 01, 02, 04, 08, 11, 14 |
| REST and OpenAPI | 01, 02, 04, 05, 06, 08, 09, 10, 11, 14, 15 |
| OAuth2/JWT and RBAC | 01, 05, 06, 08, 10, 13, 15 |
| PostgreSQL | 01, 05, 06, 07, 08, 09, 10, 11, 14, 15 |
| MongoDB | 13 |
| Redis | 02, 05, 06, 07, 10, 13, 15 |
| Kafka and event-driven design | 05, 07, 13 |
| API gateway | 05, 10, 15 |
| Resilience patterns | 05, 07, 10, 13, 15 |

### Frontend engineering

| Capability | Primary evidence projects |
|---|---|
| React and TypeScript | 01, 02, 04, 07, 09, 11, 13, 14 |
| Angular, TypeScript, and RxJS | 06, 08, 10, 15 |
| Responsive component architecture | All user-facing projects |
| Accessible UI | All user-facing projects |
| Typed API clients | All user-facing projects |
| Real-time UI | 02, 07, 11, 15 |
| End-to-end browser testing | All user-facing projects |

### Platform engineering

| Capability | Primary evidence projects |
|---|---|
| Docker and Compose | 01, 02, 05–15 |
| Kubernetes and Helm | 12, 15; selected deployment targets |
| Terraform and AWS | 12 |
| GitHub Actions | Every active implementation repository |
| Prometheus and Grafana | 05, 07, 11, 12, 15 |
| OpenTelemetry | 01, 02, 04–07, 10–15 |
| Deployment rollback and health checks | 12 and all deployed services |
| SBOM and container scanning | Every containerized release |

## Compatibility policy

- Java services target Java 21 LTS.
- Python projects declare a supported runtime range and use locked dependencies.
- Node projects declare an LTS runtime; local Node 26 may be used only after dependency compatibility is verified.
- TypeScript strict mode is required.
- PostgreSQL extensions are migration-managed.
- Container images pin stable major/minor bases and are scanned.
- GitHub Actions pin major versions initially and commit SHAs where supply-chain risk justifies it.
- Cloud features have a local verification path wherever practical.

## Technology-selection rules

- LangChain is used for integrations when it reduces custom glue; domain logic remains framework-independent.
- LangGraph is used for explicit durable workflow graphs, not simple request/response chains.
- Kafka is not used as a task queue for every background operation.
- Redis is not a substitute for durable relational state.
- Microservices are not created solely to increase service count.
- Kubernetes is a deployment target, not a local development requirement.
- External LLMs are adapters; CI uses deterministic fakes or local fixtures.
