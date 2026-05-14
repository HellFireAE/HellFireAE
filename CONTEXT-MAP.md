# Context Map

## Contexts

- [git-orchestrator](./CONTEXT.md) — root orchestrator: planning, task tracking, architectural decisions
- [your-project](./src/[your-project]/CONTEXT.md) — project submodule (replace with your actual project)

## Relationships

- **orchestrator → your-project**: orchestrator mounts project as submodule at `src/[your-project]`; orchestrator commits track submodule pointer updates
- **orchestrator ← issue tracker**: external issue tracker is source of truth for all work items; daily logs reference work item IDs
- **orchestrator → GitHub Issues**: canonical AI-automation interface; Issues mirror/extend external work items for orchestration

## Local dev

See ADR 0006 for local development environment setup.
