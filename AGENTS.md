# git-orchestrator

## Purpose
A personal orchestrator repository that manages project submodules, tracks daily work against an issue tracker, and records architectural decisions at the orchestrator level. It does not contain production code directly — instead it mounts client and personal projects as git submodules under `src/<repo-name>`, keeping planning and automation infrastructure in one place while each project retains its own git history, branch strategy, and deployment pipeline.

## Key Files
| File | Description |
|------|-------------|
| `TASKS.md` | Forward-looking backlog of upcoming work items (planned but not started) |
| `GLOSSARY.md` | Canonical term definitions for orchestrator concepts (Project, Work Item, Daily Log, HITL tags, etc.) |
| `LANGUAGE.md` | Rejected framings, behavioral rules, and resolved ambiguities for AI agents |
| `CONTEXT.md` | Relationships, examples, Tags reference, and HITL classification framework |
| `CONTEXT-MAP.md` | High-level map of bounded contexts and their relationships |
| `RULES.md` | Operational rules: AI agent file ownership, read permissions, debate execution order |

## Subdirectories
| Directory | Purpose |
|-----------|---------|
| `docs/` | Planning records: ADRs (orchestrator-level) and daily work logs (see `docs/AGENTS.md`) |
| `src/` | Git submodules — one per mounted project (see `src/AGENTS.md`) |

## For AI Agents

### Working In This Directory
- This is the **orchestrator** repo. Never add project source code here directly; all code lives inside submodules under `src/`.
- All commits follow `tag: Description` format (Conventional Commits style, no scope, no footer). Valid tags: `feat`, `fix`, `bug`, `chore`, `docs`, `style`, `refactor`, `perf`, `test`, `infra`.
- The orchestrator operates on a single `main` branch with no feature branches. Submodules provide the isolation that would otherwise require branching.
- When updating a submodule pointer, commit the `.gitmodules` change and submodule pointer update atomically with a meaningful message.

### Common Patterns
- New daily work goes in `docs/tasks/YYYY-MM-DD.md` seeded from `docs/tasks/YYYY-MM-DD.md` (template).
- Planned work items belong in `TASKS.md` until work begins; then they move to the daily log.
- ADRs belong in `docs/adr/` and cover orchestrator-level decisions only. Project-level decisions live inside the submodule's own `docs/adr/`.

### Domain Language Maintenance

AI agents working in this repo maintain living documentation inline as decisions crystallise. Do not batch — capture as they happen.

**Challenge against the glossary.** When a term conflicts with an existing definition in `GLOSSARY.md`, call it out immediately. "Your glossary defines X as Y, but you seem to mean Z — which is it?"

**Sharpen fuzzy language.** When vague or overloaded terms appear, propose the canonical term from `GLOSSARY.md`. "You're saying 'account' — do you mean the Customer or the User? Those are different things."

**Cross-reference with code.** When behavior is stated, check whether the code agrees. If a contradiction is found, surface it: "Your code does X, but you just said Y — which is right?"

**Update docs inline.**
- Term resolved → add to `GLOSSARY.md` immediately. Format: alphabetical, one sentence per term, `_Avoid_` line for aliases.
- Relationship or ambiguity resolved → update `CONTEXT.md` immediately. Format: Relationships (bold terms, cardinality), Example dialogue, Flagged ambiguities.
- Rejected framing or cross-cutting rule resolved → add to `LANGUAGE.md` immediately. Format: Principles (imperatives), Rejected framings (why not + what instead).
- Domain experts only — never couple to implementation details.

**Create files lazily.** No `CONTEXT.md` → create when first relationship or ambiguity is resolved. No `GLOSSARY.md` → create when first term is resolved. No `LANGUAGE.md` → create when first rejected framing or cross-cutting principle emerges. No `docs/adr/` → create when first ADR is needed.

**Migration.** If `CONTEXT.md` has a `Language` section, migrate all terms to `GLOSSARY.md` at the start of the session. Announce briefly ("Moving N terms from `CONTEXT.md` to `GLOSSARY.md`"), then proceed. Remove the `Language` section from `CONTEXT.md` after migrating.

**Record ADRs for hard decisions.** ADRs are the immutable log that stops decisions being re-litigated. When a decision meets all three criteria — (1) hard to reverse, (2) surprising without context, (3) result of a real trade-off — write the ADR immediately, in the session where the decision was made. Don't defer. A future agent reading `docs/adr/` can cite the ADR to close the same debate in seconds. Format: `docs/adr/NNNN-slug.md` — Status / Context / Decision / Considered Options / Consequences. Never edit an existing ADR to reverse a decision — write a new one that supersedes it.

**Offer ROADMAP.md when milestones emerge.** When multi-month milestones or outcomes not tracked in the issue tracker surface. Format: Vision / Phases (Theme, Target month, milestones) / Current Focus.

_Detailed format specs: [`docs/GLOSSARY-FORMAT.md`](./docs/GLOSSARY-FORMAT.md), [`docs/CONTEXT-FORMAT.md`](./docs/CONTEXT-FORMAT.md), [`docs/LANGUAGE-FORMAT.md`](./docs/LANGUAGE-FORMAT.md), [`docs/ADR-FORMAT.md`](./docs/ADR-FORMAT.md), [`docs/ROADMAP-FORMAT.md`](./docs/ROADMAP-FORMAT.md)._

## Dependencies

### Internal
- `src/[your-project]/` — project submodule; orchestrator tracks its HEAD pointer

### External
- Issue tracker (e.g. JIRA at `[your-instance].atlassian.net`) — source of truth for all work items; work item IDs (e.g. `PROJ-42`) appear in daily logs

<!-- MANUAL: Any manually added notes below this line are preserved on regeneration -->
