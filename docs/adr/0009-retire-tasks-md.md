# Retire TASKS.md; planned work lives in the issue tracker only

## Status
Accepted

## Context
ADR 0003 established `TASKS.md` as the forward-looking backlog, living in the orchestrator root as "the bridge to any external ticket system." In practice this created two places to check for planned work — the external issue tracker (source of truth per `CONTEXT.md`) and this local file — with no automated sync between them. The bridge never got automated, so `TASKS.md` just drifted as a second, easily-stale copy of intent that already lived in the tracker.

This does not touch the other half of ADR 0003 — Daily Logs (`docs/tasks/YYYY-MM-DD.md`) still live in the orchestrator root and still record in-progress/completed work with commit SHAs. Only the forward-looking backlog file is retired.

Same decision, made identically at the orchestrator root (see the root's `docs/adr/0008-retire-tasks-md.md`) — recorded here too since this workspace has its own independent ADR sequence.

## Decision
`TASKS.md` is deleted from this workspace root. Planned-but-not-started work is tracked directly in the external issue tracker / GitHub Issues — no local backlog file mirrors or bridges it.

## Considered Options
- **Keep `TASKS.md` and actually build the sync bridge to the issue tracker** — rejected: more automation to build and maintain for a problem that goes away entirely by just not having a second copy.
- **Keep `TASKS.md` for the small subset of work that isn't yet tracker-worthy (napkin ideas)** — rejected: reintroduces the exact ambiguity ("is this the real backlog or not") that caused the drift in the first place.

## Consequences
- One less file to keep in sync; "what's planned" has exactly one answer (the tracker) instead of two.
- `ROADMAP-FORMAT.md`'s "tactical" tier (previously `TASKS.md`) now maps to the issue tracker instead — `ROADMAP.md`, if adopted, tracks against tracker milestones, not a local file.
- Daily Logs (`docs/tasks/YYYY-MM-DD.md`) are unaffected and remain the record of in-progress/completed work.
- ADR 0003 is superseded only with respect to the backlog half of its decision; its Daily Log rationale still stands.
