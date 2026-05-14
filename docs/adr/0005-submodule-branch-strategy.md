# Sub-submodule branch strategy: feature branch → main via PR

## Status
Accepted

## Context
When a Project contains a nested git submodule (sub-submodule) with an external owner or lead developer who owns `main`, direct pushes to `main` bypass peer review and likely violate branch protection rules.

## Decision
All work branches off `main`, is pushed to a feature or contributor branch, and enters `main` only via an approved Pull Request. No direct pushes to `main`.

## Considered Options

- **Direct push to main** — rejected: bypasses lead dev review; branch protection likely enforced; unprofessional without peer review
- **Per-ticket branches** — valid alternative; adapt the branch naming convention to the team's existing conventions

## Consequences

- AI agents must checkout or create the contributor branch before writing any code in the sub-submodule
- Commits made on local `main` must be cherry-picked to the contributor branch before push
- After pushing, create a PR targeting `main` on the host platform (GitHub, Azure DevOps, etc.)
- The orchestrator's submodule pointer in `src/[your-project]` tracks the outer repo; the inner sub-submodule pointer update should follow after the PR merges to main
