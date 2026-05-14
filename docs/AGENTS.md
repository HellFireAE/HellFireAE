<!-- Parent: AGENTS.md -->

# docs

## Purpose
Central planning directory for the orchestrator. Contains two concerns: architectural decision records (ADRs) that document hard-to-reverse decisions made at the orchestrator level, and daily work logs that record in-progress and completed work items per day. Neither project source code nor project-level ADRs belong here — those live inside the respective submodule.

## Key Files
| File | Description |
|------|-------------|
| `GLOSSARY-FORMAT.md` | Format spec for GLOSSARY.md entries |
| `CONTEXT-FORMAT.md` | Format spec for CONTEXT.md structure |
| `LANGUAGE-FORMAT.md` | Format spec for LANGUAGE.md rules |
| `ADR-FORMAT.md` | Format spec and criteria for ADRs |
| `ROADMAP-FORMAT.md` | Format spec for ROADMAP.md |

## Subdirectories
| Directory | Purpose |
|-----------|---------|
| `adr/` | Architectural Decision Records for the orchestrator (see `adr/AGENTS.md`) |
| `tasks/` | Daily work logs, one file per day, plus a template (see `tasks/AGENTS.md`) |

## For AI Agents

### Working In This Directory
- Format spec files (`*-FORMAT.md`) live here — read-only reference, do not modify.
- New ADRs go in `adr/`. New daily logs go in `tasks/`. Do not create other files directly in `docs/`.
- ADRs cover **orchestrator-level** decisions only (git workflow, commit conventions, task tracking location). Project decisions belong in `src/<repo>/docs/adr/`.
- Daily logs follow the filename pattern `YYYY-MM-DD.md`. Copy `tasks/YYYY-MM-DD.md` as the template for new days.

### Common Patterns
- ADR filenames: zero-padded four-digit sequence number followed by a short kebab-case title (e.g. `0001-git-workflow.md`).
- Daily log line items carry a tag prefix (`feat`, `fix`, `chore`, etc.) matching the Conventional Commits type that will appear in the resulting commit message.
- Completed line items are marked `[x]`; in-progress or planned items remain `[ ]`.

<!-- MANUAL: Any manually added notes below this line are preserved on regeneration -->
