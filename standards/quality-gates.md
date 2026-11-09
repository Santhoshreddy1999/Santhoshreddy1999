# Project Quality Gates

Mark a gate only after the named verification has run.

## Source and dependencies

- [ ] Source implements the documented vertical slice.
- [ ] Runtime and tool versions are declared.
- [ ] Dependencies install from a clean environment.
- [ ] Lock files are committed.
- [ ] Generated artifacts have a reproducible source.

## Build and static quality

- [ ] Formatting passes.
- [ ] Linting passes.
- [ ] Type checks or compilation pass.
- [ ] Backend production build passes.
- [ ] Frontend production build passes.

## Tests

- [ ] Unit tests execute and pass.
- [ ] Database integration tests execute and pass.
- [ ] External-adapter contract tests execute and pass.
- [ ] Authorization and ownership isolation tests pass.
- [ ] Frontend component tests execute and pass.
- [ ] Critical browser journey passes.
- [ ] Failure and recovery paths are exercised.

## Data

- [ ] Migrations apply to an empty database.
- [ ] Upgrade path from the previous release is tested where applicable.
- [ ] Constraints enforce critical invariants.
- [ ] Seed/fixture data is synthetic and safe.
- [ ] Backup and restore procedure is documented for deployed data.

## API and integration

- [ ] OpenAPI or AsyncAPI reflects implementation.
- [ ] Frontend communicates with the real backend.
- [ ] Authentication and error responses are verified.
- [ ] Idempotency, timeout, retry, and pagination behavior are verified where applicable.

## Containers

- [ ] Images build.
- [ ] Images run as a non-root user where possible.
- [ ] Compose environment reaches healthy state.
- [ ] Persistent data survives an application restart.
- [ ] Images contain no embedded secret.
- [ ] Vulnerability findings are reviewed.

## Security

- [ ] Threat model exists.
- [ ] Secret scan passes.
- [ ] Dependency review is complete.
- [ ] Inputs, uploads, and generated output are validated.
- [ ] Cross-user/cross-tenant access is rejected.
- [ ] Logs and traces are checked for sensitive data.
- [ ] AI prompt-injection/tool-abuse tests pass where applicable.
- [ ] No unresolved critical or high finding remains without an explicit risk decision.

## Operations

- [ ] Structured logs include correlation identifiers.
- [ ] Health/readiness checks work.
- [ ] Key metrics are emitted.
- [ ] Trace context propagates across boundaries.
- [ ] Runbook and rollback procedure exist for deployed systems.

## Documentation and release

- [ ] README commands were replayed from a clean clone.
- [ ] Architecture diagrams match implementation.
- [ ] Implemented, in-progress, and planned features are separated.
- [ ] Environment variables are documented.
- [ ] Known limitations are stated.
- [ ] CI passes.
- [ ] Deployment status is factual.
- [ ] Release notes are useful.
- [ ] Version tag points to the verified commit.
