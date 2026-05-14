<!-- Parent: docs/AGENTS.md -->

# docs/adr

## Purpose
Architectural Decision Records for the orchestrator. Each file documents a single hard-to-reverse or surprising decision made at the orchestrator level, including the options considered and consequences accepted. ADRs here cover only orchestrator infrastructure concerns (git workflow, commit conventions, task-tracking location); project-level ADRs live inside the respective submodule at `src/<repo>/docs/adr/`.

## Key Files
| File | Description |
|------|-------------|
| `0001-git-workflow.md` | Trunk-based workflow with no feature branches; submodules provide per-project isolation |
| `0002-commit-convention.md` | `tag: Description` commit format (no scope, no footer); tags mirror Daily Log line-item prefixes |
| `0003-task-tracking-in-root.md` | Daily logs and backlog centralised in orchestrator root, not inside submodules |
| `0004-hitl-task-classification.md` | Three-tier HITL classification (`[HOOTL]`, `[HITLFE]`, `[HIC]`) governing when agents proceed vs. pause for human input |
| `0005-submodule-branch-strategy.md` | Sub-submodule branch strategy: feature branch with PR into `main`; no direct pushes to main |
| `0006-local-dev-environment.md` | Local development stack setup and constraints |

## For AI Agents

### Working In This Directory
- ADR files are immutable records of past decisions. Do not edit an existing ADR to reverse a decision — write a new ADR that supersedes the old one and references it by number.
- Filename pattern: `NNNN-kebab-case-title.md` where `NNNN` is a zero-padded sequence number one higher than the current maximum.
- When a decision is superseded, add `Superseded by [NNNN](NNNN-new-adr.md)` to the old ADR's `## Status` section.

### Canonical ADR Format

```markdown
# Title

## Status
Accepted  <!-- or: Superseded by [NNNN](NNNN-title.md) -->

## Context
What problem existed and what constraints shaped the decision.

## Decision
The specific choice made, stated as a completed fact ("The orchestrator uses…").

## Considered Options
- **Option A** — rejected: reason
- **Option B** — rejected: reason

## Consequences
Trade-offs accepted as a result of this decision — what is now easier, harder, or required.
```

### Common Patterns
- Files are plain Markdown with no front matter.
- Decisions are stated as completed facts ("The orchestrator uses…"), not proposals.
- Only write an ADR when the decision is hard to reverse, surprising without context, and the result of a real trade-off. Skip ADRs for obvious or easily-changed choices.

<!-- MANUAL: Any manually added notes below this line are preserved on regeneration -->
