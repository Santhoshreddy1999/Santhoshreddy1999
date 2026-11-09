# Contributing

## Workflow

1. Open or reference an issue with acceptance criteria.
2. Create a short-lived branch from the default branch.
3. Make a focused change with tests and documentation.
4. Run the repository's documented checks.
5. Use Conventional Commits.
6. Open a pull request and include actual verification evidence.

Branch examples:

- `feat/hybrid-retrieval`
- `fix/citation-ownership`
- `docs/deployment-runbook`
- `test/upload-limits`
- `chore/dependency-update`

Commit examples:

- `feat(retrieval): add reciprocal rank fusion`
- `fix(auth): enforce document ownership`
- `test(api): cover unsupported upload types`
- `docs(architecture): record vector store decision`

## Pull requests

Keep pull requests reviewable. Explain:

- The problem and scope.
- Material architecture/security decisions.
- Commands run and their result.
- Database, API, configuration, or deployment impact.
- Remaining limitations.

Do not include:

- Real credentials or personal data.
- Generated contribution noise.
- Unrelated formatting or refactoring.
- Claims for tests or deployments that were not executed.

## Quality

The applicable checklist in `standards/quality-gates.md` must be considered before release. A gate stays unchecked when the environment cannot verify it.

## Security

Do not open a public issue for a suspected vulnerability involving credentials, personal data, authorization bypass, or code execution. Follow `SECURITY.md`.
