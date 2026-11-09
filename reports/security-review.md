# Portfolio Security Review

**Updated:** 2026-11-09
**Scope:** Static review of the five public repositories and planned portfolio security baseline
**Not included:** Private repositories, account settings, repository secrets, collaborators, organization policy, live infrastructure, and penetration testing

## Executive result

No high-confidence active password, API key, cloud access key, private key, or GitHub token was found in tracked public content.

The absence of credentials does not make the portfolio secure. The current highest risks are:

1. Public personal and academic data in the historical `ai-project` archive.
2. Stored cross-site scripting paths in the `Santhosh-projects` vault reader.
3. Insecure educational examples that normalize browser `localStorage` for bearer and refresh tokens.
4. Missing dependency pinning, Content Security Policy, Subresource Integrity, security tests, CI scans, security policies, and update automation.
5. Misleading product claims that could cause reviewers to assume controls exist when no implementation exists.

## Findings

### Critical — untrusted Markdown can execute script

Affected repository: `Santhosh-projects`

The generated vault reader:

- Converts Markdown and inserts it through `innerHTML`.
- Does not sanitize rendered HTML.
- Allows unescaped wiki-link labels in generated markup.
- Runs Mermaid with `securityLevel: 'loose'`.

Impact:

- A malicious or compromised note can execute JavaScript when the generated reader is opened.
- Local storage, browser-accessible data, and same-origin resources could be exposed.

Required remediation:

- Use a maintained sanitizer with an allow list.
- Escape wiki-link labels and generated attributes.
- Use strict Mermaid security.
- Add adversarial fixtures and browser tests.
- Add a restrictive Content Security Policy.

### High — personal data in public coursework archive

Affected repository: `ai-project`

The Word documents contain student names/identifiers, course and institution details, and document/device metadata.

Impact:

- Unnecessary personal-data exposure.
- Search-engine and archive persistence.

Required remediation:

- Preserve a private original if needed.
- Redact personal and academic identifiers.
- Strip document metadata.
- Replace legacy binary documents with a sanitized summary or archive the repository.
- History rewriting or deletion requires explicit approval because it is destructive.

### High — unsafe token-storage examples

Affected repository: `Santhosh-projects`

Several educational snippets store access or refresh credentials in `localStorage` without sufficiently explaining the XSS trade-off.

Impact:

- Readers may copy an unsafe authentication design.
- It conflicts with the portfolio's secure-engineering claim.

Required remediation:

- Prefer `HttpOnly`, `Secure`, `SameSite` cookie patterns where architecture permits.
- Document CSRF and XSS trade-offs.
- Clearly label intentionally simplified examples.

### High — third-party scripts lack supply-chain controls

Affected repository: `Santhosh-projects`

The reader and architecture guide load scripts from CDNs without CSP, Subresource Integrity, or a documented dependency-update process. One page uses a mutable major-version URL.

Required remediation:

- Pin exact versions and integrity hashes or self-host build artifacts.
- Add CSP and referrer policy.
- Add package metadata, lock file, dependency updates, and vulnerability review.

### Medium — committed workspace and external identifiers

Affected repository: `Santhosh-projects`

- Obsidian workspace state records active/recent files.
- Multiple third-party document identifiers are public.

Required remediation:

- Remove workspace state from tracking and add it to `.gitignore`.
- Review link ownership, access, and redistribution rights.

### Medium — no security governance

Affected repositories: all five

Missing:

- `SECURITY.md`.
- Threat models.
- Dependency update automation.
- Secret scanning workflow.
- SAST and container scanning.
- Supported-version policy.
- Vulnerability disclosure process.

### Informational — local Git metadata

Local clone reflogs contain the configured corporate email address. Reflogs are not normally pushed, but repositories are located inside a synchronized directory. Local backup and retention policy should be reviewed.

No email address is intentionally copied into the new portfolio content.

## AI security baseline

Every AI project will address:

- Prompt injection from users and retrieved content.
- Data exfiltration through tools or model providers.
- Cross-user and cross-tenant retrieval.
- Excessive agency and unauthorized writes.
- Unbounded token, cost, recursion, and tool execution.
- Sensitive data in prompts, outputs, traces, and evaluation datasets.
- Unsafe or malformed structured output.
- Model/provider outage, timeout, and rate limiting.
- Citation fabrication and unsupported claims.
- Poisoned documents and evaluation data.

Required controls:

- Treat retrieved content as data, never as privileged instructions.
- Separate system policy, user input, retrieved context, and tool output.
- Validate all model-produced structured data.
- Enforce ownership in the database query, not only in prompts.
- Give tools narrow, typed, deny-by-default permissions.
- Require human approval for sensitive writes.
- Apply time, token, recursion, network, and monetary budgets.
- Record redacted audit events.
- Provide deterministic test doubles and adversarial tests.

## Application security baseline

- Passwords use an adaptive password hash.
- Authentication errors do not disclose account existence unnecessarily.
- Tokens and sessions have expiry, rotation, and revocation behavior.
- Browser refresh credentials avoid JavaScript-readable storage where practical.
- Object-level authorization is mandatory.
- Inputs, uploads, and archive contents have size and type limits.
- Uploaded file names never control filesystem paths.
- SQL uses parameterized queries and ORM/query-builder safeguards.
- CORS is explicit by environment.
- Rate limits protect authentication, uploads, model requests, and expensive searches.
- Errors returned to clients exclude stack traces and secrets.
- Logs use structured fields and redact sensitive values.
- Production containers run as non-root with minimal images and read-only filesystems where possible.

## Secret-management baseline

- `.env.example` contains names and safe placeholders only.
- `.env`, key files, credentials, local databases, and generated secrets are ignored.
- CI uses repository/environment secrets with least privilege.
- Cloud deployments use a managed secret store and workload identity.
- No secret is passed as a Docker build argument.
- Rotation and revocation instructions are documented.

## Security verification gates

Planned automated checks:

- Secret scanning.
- Dependency vulnerability review.
- Static analysis.
- Infrastructure and container scanning.
- SBOM generation.
- Upload and parser abuse tests.
- Cross-user authorization tests.
- Prompt-injection and tool-policy tests.
- Browser CSP and XSS tests.

## Current risk disposition

- `ai-project` privacy exposure: open; no destructive remediation performed.
- `Santhosh-projects` XSS path: open; repository not modified during initial audit.
- Placeholder repository claims: open; profile will not feature them as completed.
- New Project 01 risks: core local controls implemented and exercised; CSRF
  hardening, rate limits, stronger parser resource limits, CI scans, live
  provider review, and browser security automation remain open.

## Project 01 local security evidence

Verified on 2026-11-09:

- Argon2 password hashing.
- Signed, expiring `HttpOnly` cookie authentication.
- No browser Web Storage token persistence.
- Explicit credentialed CORS allow list.
- Query-level per-user ownership across documents, conversations, retrieval,
  evaluation, and deletion.
- Two-user isolation in API tests and deployed smoke testing.
- Bounded upload and parsed-content validation for supported file types.
- Retrieved content labeled as untrusted data.
- Persisted citation-to-chunk provenance.
- Provider keys accepted only through backend runtime configuration.
- Generic provider and internal errors.
- Structured request logs without document or credential payloads.
- PostgreSQL not published to the host.
- Non-root backend and frontend application images.
- CI secret scan passed on the release commit.
- Protected `main` requires six build, test, image, and integration checks and
  disallows force pushes and deletion.

The specialized security-review subagent could not compute a diff because the
new repository had no initial commit and all source was untracked. The threat
model and static/manual checks were completed, but this does not substitute for
an independent post-commit review.

## Security claim policy

A project may say “security considerations documented” when a threat model exists. It may say “security tested” only when the named automated or manual checks have run. It may not say “secure,” “enterprise-grade,” or “production-ready” solely because it uses authentication, containers, or a security framework.

## Public portfolio website

Verified on 2026-11-09:

- Static deployment with no runtime API, authentication, analytics, or secret.
- Content Security Policy, strict referrer policy, and HTTPS-enforced Pages.
- External-link safety tests.
- Public phone and residential address deliberately omitted.
- Email and LinkedIn published from the supplied current resume.
- Certificate title corrected to the independently verified Anthropic
  “Introduction to Model Context Protocol.”
- Resume conflicts and self-reported metrics documented in the repository's
  content-integrity record.
- Protected `main` and passing lint/type/test/build/deploy workflow.
