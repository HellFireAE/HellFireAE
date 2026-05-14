# Orchestrator Architecture

This is a personal orchestrator repository. It owns planning, tracking, and tooling — not production code. All project code lives in git submodules under `src/`.

## Structure

```
orchestrator (main)
├── ARCHITECTURE.md   ← this file; living map of current system state
├── TASKS.md          ← forward-looking backlog
├── CONTEXT.md        ← domain relationships and examples
├── CONTEXT-MAP.md    ← bounded context index (multi-context repo)
├── GLOSSARY.md       ← canonical term definitions
├── LANGUAGE.md       ← rejected framings and behavioral rules
├── docs/
│   ├── adr/          ← orchestrator-level architectural decisions (immutable)
│   └── tasks/        ← daily work logs (YYYY-MM-DD.md)
└── src/
    └── <repo>/       ← one git submodule per project
```

## Orchestrator responsibilities

| Concern | Location |
|---------|----------|
| Forward planning | `TASKS.md` |
| Daily work tracking | `docs/tasks/YYYY-MM-DD.md` |
| Architectural decisions | `docs/adr/` |
| Domain language | `GLOSSARY.md`, `LANGUAGE.md` |
| Submodule tracking | `src/<repo>/` pointer commits |
| AI agent governance | HITL classification (see ADR 0004) |

## Projects (submodules)

Replace this table with your actual projects:

| Path | Remote | Branch strategy |
|------|--------|----------------|
| `src/<your-project>/` | GitHub / Azure / etc. | See ADR 0005 if sub-submodules exist |

## Commit flow

Innermost-first — commit and push from deepest submodule outward:

1. Sub-submodule (if any) → push contributor branch, open PR into `main`
2. After PR merges: project submodule → update sub-submodule pointer, push `main`
3. Orchestrator → update project pointer, push `main`

Reversing the order creates redundant pointer-update commits (see ADR 0001).

## Planning → execution pipeline

```
External tracker (source of truth) → TASKS.md (backlog) → Daily Log → commit
```

Work items enter `TASKS.md` when planned, move to the day's Daily Log when started, and close on lead-developer sign-off — not on commit (see ADR 0003).

## ADR index

| ADR | Decision |
|-----|---------|
| [0001](docs/adr/0001-git-workflow.md) | Trunk-based workflow; submodules as isolation layer |
| [0002](docs/adr/0002-commit-convention.md) | `tag: Description` commit format |
| [0003](docs/adr/0003-task-tracking-in-root.md) | Planning centralised in orchestrator root |
| [0004](docs/adr/0004-hitl-task-classification.md) | HOOTL/HITLFE/HIC classification |
| [0005](docs/adr/0005-submodule-branch-strategy.md) | Feature branch → PR into `main` for sub-submodules |
| [0006](docs/adr/0006-local-dev-environment.md) | Docker stack + reverse proxy for local dev |
