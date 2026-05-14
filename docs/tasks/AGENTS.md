<!-- Parent: docs/AGENTS.md -->

# docs/tasks

## Purpose
Daily work logs for the orchestrator. Each file named `YYYY-MM-DD.md` records in-progress and completed work items for that day, with line items tagged by Conventional Commits type. The file `YYYY-MM-DD.md` is the template for seeding new daily logs. Completed items carry commit SHAs inline for traceability. Forward-looking planned work lives in `TASKS.md` at the repo root, not here.

## Key Files
| File | Description |
|------|-------------|
| `YYYY-MM-DD.md` | Template for new daily logs — copy and rename before adding entries |

## For AI Agents

### Working In This Directory
- To start a new day: copy `YYYY-MM-DD.md` to today's date filename, then fill in the work item sections.
- Each line item format: `- [x] tag: Description` (completed) or `- [ ] tag: Description` (planned/in-progress).
- Valid tags: `feat`, `fix`, `bug`, `chore`, `docs`, `style`, `refactor`, `perf`, `test`, `infra`.
- Group line items under `### [WORK-ITEM-ID] Work Item Title` headings, grouped under `## repo-name` sections.
- Do not move work items here from `TASKS.md` until work actually begins.

### Common Patterns
- File naming: `YYYY-MM-DD.md` using ISO 8601 date of the work day.
- Commit SHAs are appended inline to completed line items for traceability (e.g. `feat: Add block \`a3f9c12\``).

<!-- MANUAL: Any manually added notes below this line are preserved on regeneration -->
