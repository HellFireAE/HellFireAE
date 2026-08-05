# Orchestrator Architecture

This is a personal orchestrator repository. It owns planning, tracking, and tooling — not production code. All project code lives in git submodules under `src/`.

## Structure

```
orchestrator (main)
├── ARCHITECTURE.md   ← this file; living map of current system state
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
| Forward planning | External issue tracker / GitHub Issues (see ADR 0009) |
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
External tracker (source of truth) → Daily Log → commit
```

Work items live in the external issue tracker while planned; they enter the day's Daily Log when started, and close on lead-developer sign-off — not on commit (see ADR 0003, ADR 0009).

## ADR index

| ADR | Decision |
|-----|---------|
| [0001](docs/adr/0001-git-workflow.md) | Trunk-based workflow; submodules as isolation layer |
| [0002](docs/adr/0002-commit-convention.md) | `tag: Description` commit format |
| [0003](docs/adr/0003-task-tracking-in-root.md) | Planning centralised in orchestrator root |
| [0004](docs/adr/0004-hitl-task-classification.md) | HOOTL/HITLFE/HIC classification |
| [0005](docs/adr/0005-submodule-branch-strategy.md) | Feature branch → PR into `main` for sub-submodules |
| [0006](docs/adr/0006-local-dev-environment.md) | Docker stack + reverse proxy for local dev |
| [0007](docs/adr/0007-independent-ai-agent-files.md) | CLAUDE.md/GEMINI.md/QWEN.md independent, never symlinks |
| [0008](docs/adr/0008-dotfiles-into-hermes-operator.md) | Dotfiles live in the Hermes Operator, not a separate template repo |
| [0009](docs/adr/0009-retire-tasks-md.md) | `TASKS.md` retired; planned work lives in the issue tracker only |
