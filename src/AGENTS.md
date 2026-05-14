<!-- Parent: AGENTS.md -->

# src

## Purpose
Container for all project submodules. Each subdirectory is a separate git repository mounted via `git submodule`, with its own remote, branch strategy, and deployment pipeline. The orchestrator tracks only the submodule HEAD pointer; all project code, history, and project-level documentation live inside the submodule itself.

## Subdirectories
| Directory | Purpose |
|-----------|---------|
| `[your-project]/` | Replace with your project submodule (see `[your-project]/AGENTS.md`) |

## For AI Agents

### Working In This Directory
- Never create files directly in `src/` — content belongs inside a submodule.
- To update a submodule to its latest commit: `git submodule update --remote src/<repo-name>`, then commit the pointer change in the orchestrator with a meaningful message.
- If a submodule remote URL changes, update `.gitmodules` at the root and run `git submodule sync`.
- Each submodule has its own AGENTS.md / CONTEXT.md — read those before working inside the submodule.

### Common Patterns
- Submodule directories are named after the project domain (e.g. `example.com` or `my-project`).
- Orchestrator commits that update a submodule pointer use the `chore` or `infra` tag: e.g. `chore: Update [your-project] submodule pointer`.

<!-- MANUAL: Any manually added notes below this line are preserved on regeneration -->
