# Task tracking centralised in the orchestrator repo

## Status
Accepted

## Context
Work spans multiple projects simultaneously. Without a single planning location, cross-project status is invisible at meeting time and automation has no stable entry point.

## Decision
Daily work logs (`docs/tasks/YYYY-MM-DD.md`) and the forward-looking backlog (`TASKS.md`) live in the orchestrator root, not inside individual project submodules. Project repos contain only code.

## Considered Options

- **Per-project task files inside each submodule** — rejected: cross-project work becomes invisible; meeting prep requires aggregating from multiple repos; no single automation entry point
- **External task tool only** — rejected: lacks the granularity and git-linkage needed for daily commit traceability; AI agents have no reliable local interface

## Consequences

- `TASKS.md` is the forward-looking backlog and the bridge to any external ticket system; Daily Logs record completed and in-progress items with commit SHAs inline for traceability
- Cross-project work is surfaceable in one place at meeting time
- The orchestrator root is the natural interface for future automation
