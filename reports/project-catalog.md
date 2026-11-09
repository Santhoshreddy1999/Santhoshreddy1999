# Project Catalog

**Updated:** 2026-11-09
**Catalog status:** Planned portfolio; completion is tracked separately in `implementation-tracker.md`.

## Naming convention

- Lowercase kebab-case repository names.
- Product-oriented names without words such as `sample`, `demo`, `test`, or `final`.
- Technology names belong in descriptions and topics, not usually in repository names.
- A repository name must remain accurate if an implementation detail changes.

## 01 — Enterprise AI Knowledge Assistant

**Repository:** `enterprise-rag-assistant`
**Capability:** Secure, source-grounded generative AI application
**Primary stack:** Python, FastAPI, PostgreSQL, pgvector, React, Docker

Architecture:

- React single-page application.
- FastAPI application organized around domain, application, adapter, and API boundaries.
- PostgreSQL for identity, documents, conversations, evaluations, and audit records.
- pgvector for embeddings plus PostgreSQL full-text search for hybrid retrieval.
- Pluggable document parsers, embedding providers, rerankers, and chat providers.
- Background ingestion worker after the synchronous MVP is stable.

MVP:

- Register/login, upload documents, ingest text/Markdown/PDF/DOCX, ask questions, receive citations, view conversation history, and run a retrieval evaluation.
- Deterministic offline embedding and answer mode so tests do not need paid credentials.

Engineering differentiators:

- Per-user document isolation.
- Reciprocal-rank-fusion hybrid retrieval.
- Prompt-injection boundaries and citation verification.
- Evaluation dataset and measurable retrieval metrics.

## 02 — Multi-Agent AI Orchestration Platform

**Repository:** `agent-orchestration-platform`
**Capability:** Durable agent workflows with approvals and recovery
**Primary stack:** Python, LangGraph, FastAPI, Redis, React

Architecture:

- Explicit LangGraph state machine rather than open-ended agent loops.
- Planner, researcher, executor, reviewer, and policy agents.
- Redis-backed checkpoints and task queues.
- Tool registry with schemas, authorization policy, timeout, and idempotency metadata.
- Server-sent events for execution updates and a React workflow graph.

MVP:

- Submit a research task, inspect the plan, approve a sensitive tool call, observe execution, retry a failed node, and resume from a checkpoint.

Engineering differentiators:

- Bounded budgets, recursion limits, human gates, replayable traces, and failure injection tests.

## 03 — MCP Server & AI Tool Ecosystem

**Repository:** `mcp-tool-ecosystem`
**Capability:** Standards-based AI tool and context integration
**Primary stack:** Python, TypeScript, MCP, Node.js

Architecture:

- A TypeScript gateway and focused Python/TypeScript MCP servers.
- Separate resources, prompts, and tools.
- OAuth-compatible authentication boundary and per-tool authorization.
- JSON-schema validation, allow-listed filesystem/network access, and structured audit events.

MVP:

- Documentation-search, repository-inspection, and safe task-management servers integrated with an MCP client.

Engineering differentiators:

- Threat model for confused-deputy, prompt-injection, path-traversal, and data-exfiltration risks.
- Conformance and adversarial tool tests.

## 04 — AI-Powered Developer Copilot

**Repository:** `developer-intelligence-copilot`
**Capability:** Repository and pull-request intelligence
**Primary stack:** Python, FastAPI, LLMs, React, GitHub API

Architecture:

- GitHub App installation model for least-privilege repository access.
- Webhook ingestion, repository indexing, AST-aware analysis, and job workers.
- Evidence-linked findings stored with commit SHA and file location.

MVP:

- Index one authorized repository, explain selected code, summarize a pull request, propose tests, and draft documentation with source links.

Engineering differentiators:

- Untrusted-code isolation, no arbitrary repository execution, commit-pinned findings, and confidence/evidence labels.

## 05 — Enterprise Java Microservices Platform

**Repository:** `event-driven-enterprise-platform`
**Capability:** Secure, resilient Java distributed systems
**Primary stack:** Java 21, Spring Boot, Spring Security, Kafka, PostgreSQL, Redis

Architecture:

- Identity, account, order, and notification boundaries behind an API gateway.
- Database ownership per service.
- Transactional outbox and idempotent Kafka consumers.
- OpenTelemetry context propagation and resilience policies.

MVP:

- Authenticated order workflow from API request through persisted state, emitted event, and notification.

Engineering differentiators:

- Contract tests, Testcontainers, failure/retry tests, trace correlation, and documented consistency model.

## 06 — AI-Powered Customer Support Platform

**Repository:** `customer-support-intelligence`
**Capability:** Human-centered AI support operations
**Primary stack:** Angular, Spring Boot, Python, RAG, PostgreSQL, Redis

Architecture:

- Spring Boot system of record for customers, tickets, routing, and permissions.
- Python inference service for classification, sentiment, summarization, and RAG.
- Angular workspace for customer and agent experiences.

MVP:

- Create a ticket, classify and route it, suggest a cited response, escalate to a human, and measure resolution workflow.

Engineering differentiators:

- Human override, model confidence, PII redaction, audit history, and feedback-based evaluation.

## 07 — Real-Time Analytics Intelligence Platform

**Repository:** `realtime-analytics-platform`
**Capability:** Streaming analytics and anomaly detection
**Primary stack:** React, Java, Kafka, Python, PostgreSQL, Redis

Architecture:

- Schema-governed event ingestion.
- Java stream processing for windows and aggregates.
- Python anomaly service operating on derived features.
- WebSocket/SSE gateway for live React dashboards.

MVP:

- Generate synthetic events, calculate rolling metrics, display live updates, flag anomalies, and query historical aggregates.

Engineering differentiators:

- Event-time semantics, late-event policy, replay tests, schema compatibility, and backpressure visibility.

## 08 — AI Resume & Interview Intelligence Platform

**Repository:** `career-intelligence-platform`
**Capability:** Privacy-aware career analysis
**Primary stack:** Angular, FastAPI, LLMs, RAG, PostgreSQL

Architecture:

- Encrypted resume storage with explicit retention controls.
- Structured parsing pipeline and skills taxonomy.
- Evidence-grounded job matching and interview workflow.

MVP:

- Parse a synthetic resume and job description, show evidence-linked skill gaps, generate interview questions, and score a mock response against a rubric.

Engineering differentiators:

- No invented experience, explainable matching, bias evaluation, export/delete controls, and synthetic fixtures.

## 09 — AI-Powered Financial Intelligence Dashboard

**Repository:** `financial-insights-platform`
**Capability:** Explainable analytics over synthetic financial data
**Primary stack:** React, Spring Boot, Python, PostgreSQL, Docker

Architecture:

- Spring Boot transaction and budget API.
- Python categorization and forecasting service.
- React analytics dashboard.

MVP:

- Import synthetic transactions, categorize them, track budgets, show trends, generate explainable insights, and export a report.

Engineering differentiators:

- Synthetic data only, model confidence, forecasting backtests, and prominent non-advisory boundaries.

## 10 — Enterprise API Management Platform

**Repository:** `api-management-platform`
**Capability:** API lifecycle, access, quotas, and analytics
**Primary stack:** Java, Spring Boot, Kong, Redis, PostgreSQL, Angular

Architecture:

- Control plane for API registration, products, consumers, keys, and policy.
- Kong data plane.
- Redis-backed quota counters and PostgreSQL audit/analytics records.
- Angular developer and administrator portals.

MVP:

- Register an API, publish a version, issue a credential, enforce a rate limit, and inspect usage.

Engineering differentiators:

- Key rotation, hashed credentials, policy audit trail, OpenAPI validation, and gateway/config reconciliation.

## 11 — AI Observability & Evaluation Platform

**Repository:** `llm-observability-platform`
**Capability:** LLM quality, cost, latency, and trace analysis
**Primary stack:** Python, FastAPI, OpenTelemetry, Prometheus, Grafana, React

Architecture:

- OpenTelemetry-compatible ingestion API.
- Trace, span, prompt-version, token, cost, and evaluation data model.
- Prometheus operational metrics and Grafana dashboards.
- React experiment and trace explorer.

MVP:

- Instrument Project 01, compare two retrieval configurations, inspect traces, view token/cost/latency, and run prompt/RAG evaluations.

Engineering differentiators:

- PII-aware telemetry, prompt redaction, sampling, dataset versioning, and reproducible experiment reports.

## 12 — Kubernetes-Based Application Deployment Platform

**Repository:** `cloud-native-delivery-platform`
**Capability:** Repeatable cloud infrastructure and application delivery
**Primary stack:** Docker, Kubernetes, Helm, Terraform, GitHub Actions, AWS

Architecture:

- Terraform modules for network, cluster, identity, registry, and observability.
- Helm charts with probes, resources, autoscaling, disruption budgets, and network policy.
- Environment promotion with plan, approval, deploy, smoke test, and rollback.

MVP:

- Deploy a portfolio service to a local Kubernetes cluster first; add AWS only when credentials and cost controls are explicitly configured.

Engineering differentiators:

- Least-privilege workload identity, policy checks, cost notes, disaster-recovery runbook, and verified rollback.

## 13 — Intelligent E-Commerce Microservices Platform

**Repository:** `intelligent-commerce-platform`
**Capability:** Event-driven commerce with recommendation features
**Primary stack:** React, Spring Boot, Kafka, MongoDB, Redis, Docker

Architecture:

- Catalog, cart, order, inventory, payment-adapter, and recommendation boundaries.
- Saga with explicit compensation and idempotency.
- Sandbox payment provider only.

MVP:

- Browse catalog, add to cart, place sandbox order, reserve inventory, process payment outcome, and inspect order history.

Engineering differentiators:

- Oversell prevention, outbox/inbox patterns, reconciliation jobs, failure tests, and explainable recommendations.

## 14 — AI-Powered Enterprise Document Automation

**Repository:** `document-automation-platform`
**Capability:** OCR, extraction, classification, approval, and search
**Primary stack:** Python, FastAPI, React, OCR, RAG, PostgreSQL

Architecture:

- Immutable object ingestion and asynchronous processing pipeline.
- OCR, classification, extraction, confidence scoring, and validation stages.
- Human approval workflow and versioned output.

MVP:

- Ingest synthetic invoices and forms, OCR them, extract fields, route low-confidence results for review, search content, and export a report.

Engineering differentiators:

- Provenance for every extracted field, malware/content checks, retention policy, and measurable extraction quality.

## 15 — AI Full-Stack Engineering Command Center

**Repository:** `engineering-command-center`
**Capability:** Unified engineering operations and AI workflow interface
**Primary stack:** Angular, Spring Boot, Python, MCP, LangGraph, PostgreSQL, Redis, Docker, Kubernetes

Architecture:

- Angular operator console.
- Spring Boot control plane for projects, environments, permissions, and audit.
- Python agent plane for analysis and report workflows.
- MCP adapters for approved engineering tools.
- Read models for repository, CI, deployment, and telemetry status.

MVP:

- Connect approved portfolio repositories, inspect verified CI and deployment status, run an approval-gated engineering report, and trace its tool calls.

Engineering differentiators:

- It integrates existing stable services rather than duplicating them.
- Read-only defaults, explicit write approval, tenant isolation, complete tool audit, and centralized observability.

## Existing repository disposition

- `MY_Skills` → reuse as the profile and portfolio governance repository; rename to `Santhoshreddy1999`.
- `Santhosh-projects` → improve and rename to `engineering-architecture-vault`.
- `PG-management-app` → greenfield implementation only if retained; do not count the placeholder as a project.
- `CSS_Learning_App` → lower-priority greenfield or archive.
- `ai-project` → privacy-clean historical archive; do not count it as modern AI engineering evidence.

## Catalog governance

Each project README must show one of the standard statuses: Planned, In progress, MVP verified, Release candidate, Complete, Blocked, or Archived.

The catalog may describe planned architecture, but only the implementation tracker and release evidence determine what is complete.
