# Tag: Description commit format

## Status
Accepted

## Context
Commit messages must be machine-readable for tooling and AI agents, and must mirror the Daily Log line-item format to keep planning and version control in sync. The project is a single-developer orchestrator; scope identifiers add no disambiguation value.

## Decision
Commits use `tag: Description` format — no scope, no footer. Tags are drawn from the fixed set: `feat`, `fix`, `bug`, `chore`, `docs`, `style`, `refactor`, `perf`, `test`, `infra`. This directly mirrors Daily Log line-item prefixes.

```
feat: Seed tabbed content block from theme
```

## Considered Options

- **Conventional Commits with scope** (`feat(auth): ...`) — rejected: single-developer repo; scope adds noise without disambiguation benefit
- **Free-form commit messages** — rejected: breaks AI parsability and severs the link between Daily Log entries and commits

## Consequences

- Commit messages and Daily Log entries share the same tag vocabulary — no translation layer needed
- Tooling that expects a `scope` field (e.g. standard-version) requires configuration to treat scope as optional
- New tags require updating CONTEXT.md, GLOSSARY.md, and AGENTS.md simultaneously to stay in sync
