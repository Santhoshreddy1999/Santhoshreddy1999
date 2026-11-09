# Deployment Report

**Updated:** 2026-11-09
**Current verified deployments:** Project 01 local Docker Compose environment

## Executive result

No pre-transformation repository contains a verified deployment configuration,
deployment record, container image, release, or live application URL. Project
01 is now public and has a locally verified Docker Compose deployment, but it
has not been remotely deployed.

Docker, Docker Compose, and `kubectl` are available in the local environment. Terraform is not currently available on the command path. Tool availability alone is not deployment evidence.

## Existing repositories

### `ai-project`

- Deployment type: none.
- Container: none.
- Runtime manifest: none.
- Live URL: none verified.

### `CSS_Learning_App`

- Deployment type: none.
- GitHub Pages: not enabled.
- Build artifact: none.
- Live URL: none verified.

### `MY_Skills`

- Deployment type: GitHub-rendered Markdown planned.
- Remote update: not yet verified.

### `Santhosh-projects`

- Deployment type: none verified.
- The generated HTML can be opened locally, but that is not a deployment.
- No GitHub Pages or static-host configuration exists.

### `PG-management-app`

- Deployment type: none.
- Container or executable artifact: none.
- Live URL: none verified.

## Deployment status vocabulary

- **Not deployed:** no environment exists.
- **Configuration only:** manifests exist but have not been applied successfully.
- **Locally verified:** Compose or local Kubernetes deployment passed smoke checks.
- **Development deployed:** a remote development environment passed smoke checks.
- **Production-like deployed:** a controlled environment has monitoring, rollback, backup, and operational documentation.
- **Unavailable:** a previously verified deployment is currently failing; include incident status.

## Project 01 deployment plan

### Verified local result

On 2026-11-09:

- Compose configuration validated.
- Backend and frontend images built.
- PostgreSQL 16/pgvector, FastAPI, and Nginx containers reached healthy state.
- Alembic applied the initial schema.
- Direct API and same-origin Nginx-proxied smoke journeys passed.
- Registration, upload, hybrid retrieval, citations, history, retrieval
  evaluation, and cross-user isolation passed.
- Two document records survived a complete container down/up cycle while the
  named volume was retained.

This is a local development deployment, not a public or cloud deployment.

### Local application mode

- Backend and frontend development commands.
- Deterministic offline AI provider.
- Local database configuration documented.

### Docker Compose mode

Services:

- PostgreSQL with pgvector.
- FastAPI API.
- React static frontend or development server, depending on profile.
- Optional worker after asynchronous ingestion is introduced.

Checks:

- Containers reach healthy state.
- Migrations apply automatically or through a documented command.
- User registration works.
- Fixture document can be uploaded and queried.
- Restart preserves persistent data.
- Secrets are not embedded in images.

### Local Kubernetes mode

Introduced after Compose is verified:

- Deployments and services.
- ConfigMaps and Secret references.
- Readiness/liveness/startup probes.
- Requests and limits.
- Persistent data strategy documented.
- Ingress.
- Horizontal autoscaling only after measurable load behavior.

### Cloud mode

Not attempted during the initial transformation.

Before AWS deployment:

- Confirm account and credential mechanism.
- Define a budget and teardown plan.
- Use Terraform remote state with locking and encryption.
- Use workload identity instead of static cloud keys.
- Select managed PostgreSQL/vector support.
- Configure TLS, DNS, secret storage, logs, metrics, traces, backups, and alerting.
- Execute restoration and rollback drills.

## CI/CD target

Pull request:

1. Formatting, linting, and type checks.
2. Unit tests.
3. Database integration tests.
4. Frontend tests and production build.
5. Secret and dependency checks.
6. Container build.

Main branch:

1. Repeat blocking quality checks.
2. Generate SBOM and scan image.
3. Publish immutable image tag after authentication is configured.
4. Deploy only to an approved environment.
5. Run smoke tests.
6. Roll back automatically or halt promotion on failure.

Release:

- SemVer tag.
- Human-reviewed release notes.
- Image digest and provenance.
- Migration and rollback notes.
- Known limitations.

## Current blockers

- No container registry or cloud credential has been configured.
- Project 01 source is published; its images are locally verified but not
  published to a registry.
- Terraform is not installed on the current command path.

These are recorded blockers, not failed deployment claims.
