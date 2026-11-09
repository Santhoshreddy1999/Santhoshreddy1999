# Repository Engineering Standard

**Version:** 1.0
**Effective:** 2026-11-09

## Naming

- Use lowercase kebab-case.
- Prefer a product or capability name: `enterprise-rag-assistant`.
- Avoid `sample`, `demo`, `test`, `new`, `final`, dates, and personal prefixes.
- Keep names accurate if an implementation detail changes.

## Required root files

- `README.md`
- `LICENSE` when a licensing decision has been made
- `.gitignore`
- `.editorconfig`
- `.env.example` when configuration exists
- `CONTRIBUTING.md`
- `SECURITY.md`
- `CHANGELOG.md` after the first release

## Required documentation

- Problem and target users.
- Verified project status.
- Features grouped as implemented, in progress, and planned.
- Architecture and decisions.
- Local setup and exact commands.
- Environment-variable reference with safe examples.
- API and event contracts.
- Data model and migrations.
- Testing strategy and commands.
- Security and privacy considerations.
- Container and deployment instructions.
- Observability and operations.
- Known limitations and roadmap.

## Architecture

- Start with a modular monolith unless service separation has a documented reason.
- Keep domain/application code independent of frameworks where proportionate.
- Put LLMs, vector stores, external APIs, and cloud services behind explicit ports.
- Define transaction, consistency, retry, timeout, and ownership boundaries.
- Record material decisions in `docs/adr/`.
- Store Mermaid source with the documentation.

## Source layout

Use a layout native to the ecosystem. Do not force identical folders across Java, Python, and TypeScript.

Common top-level structure:

```text
.
├── .github/
├── backend/ or services/
├── frontend/
├── docs/
│   ├── adr/
│   ├── architecture.md
│   ├── deployment.md
│   ├── security.md
│   └── testing.md
├── infra/
├── scripts/
├── tests/
├── .env.example
├── compose.yaml
└── README.md
```

Omit directories that have no real content.

## Configuration and secrets

- Read environment-specific values from environment variables or a secret manager.
- Commit `.env.example`; never commit `.env`.
- Never put real tokens, passwords, private keys, connection strings, or cloud credentials in examples.
- Validate configuration at startup and fail with a safe, actionable message.
- Keep production secrets out of image layers and build arguments.

## Testing

- Unit-test domain rules and security-sensitive helpers.
- Integration-test databases, queues, caches, and external adapters through controlled substitutes.
- Contract-test APIs and events.
- Browser-test critical user journeys.
- Include failure paths, retries, authorization, and isolation.
- Do not claim coverage unless a coverage command has executed.

## CI

Pull requests should run:

- Formatting and linting.
- Type checks or compilation.
- Unit tests.
- Integration tests where supported.
- Production builds.
- Secret scanning.
- Dependency review.
- Container build/scan for containerized services.

The README must use commands equivalent to CI.

## Security

- Deny by default.
- Check object ownership in addition to roles.
- Use parameterized data access.
- Bound request, upload, prompt, tool, and output sizes.
- Sanitize rendered untrusted content.
- Redact secrets and sensitive data from logs and traces.
- Threat-model AI tools, retrieved content, and model output.
- Add `SECURITY.md` with a private reporting path when one is available.

## Observability

- Structured logs with request/correlation identifiers.
- Health and readiness endpoints for services.
- Metrics for traffic, errors, latency, saturation, and domain-critical behavior.
- Distributed traces across HTTP, events, workers, and AI calls.
- No raw sensitive prompts or documents in telemetry by default.

## Commits and branches

- Use short-lived branches: `feat/*`, `fix/*`, `docs/*`, `refactor/*`, `test/*`, `chore/*`.
- Use Conventional Commits.
- Keep each commit coherent and truthful.
- Do not backdate, split changes artificially, or generate activity for appearance.
- Use pull requests where practical and include verification evidence.

## Releases

- Use semantic versioning after the first usable release.
- Release notes list implemented changes, migrations, security impact, known limitations, and rollback considerations.
- A release tag is created only from a passing commit.
- Do not publish a deployment URL until it has been smoke-tested.

## Status labels

Use exactly one:

- Planned
- In progress
- MVP verified
- Release candidate
- Complete
- Blocked
- Archived

Planned architecture must never appear under an “implemented features” heading.
