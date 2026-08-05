# Dotfiles live in the Hermes Operator, not a separate template repo

## Status
Accepted

## Context
Machine bootstrap (shell, editor, `claude`/`codex`/`gemini`/`qwen` config, git identity, GNU Stow symlinking) previously lived in a standalone repo, `jonathanhfmills/dotfiles`. That repo had grown into a "Dotfiles Template" with a documented but never-adopted Host Fleet model (per-device forked "Host Repos" tracking an `upstream` remote via `make sync-upstream`) and a large amount of unrelated scope: a `bicameral-mind` submodule running a debate/agent/k3s/Discord pipeline, a reverse proxy stack, and device-specific `.env` profiles. Only one machine ever existed, so the fleet model was speculative complexity. The user is migrating this machine from Ubuntu to CachyOS (Arch) and wants a quick, repeatable bootstrap without re-deriving the whole stack by hand.

## Decision
Dotfile Packages (GNU Stow-managed directories: `.claude`, `.codex`, `.gemini`, `.qwen`, `git`, `tmux`, `bin`) and their Makefile bootstrap targets move into this workspace repo, the **Hermes Operator**, nested under `config/` and owned directly by the operator (not mounted as an Agency submodule) — kept out of the repo root to avoid crowding the orchestrator's own planning docs. The old `jonathanhfmills/dotfiles` repo is archived on GitHub after migration. Arch/CachyOS package-manager targets use **paru** as the AUR helper (CachyOS's own default). The `bicameral-mind` agent/debate infrastructure, reverse proxy, and device-`.env` profiles are dropped from scope — not migrated, left behind in the archived repo.

## Considered Options
- **Fork old repo as a new Host Repo (`dotfiles-desktop`) per its own documented model** — rejected: formalizes a fleet-of-devices model that was never used for more than one machine; adds an `upstream` sync step with no current second host to justify it.
- **Mount old dotfiles repo as an Agency submodule under `src/dotfiles`** — rejected: dotfiles are the Hermes Operator's own machine config, not a client/personal codebase with independent branch strategy — doesn't fit the Agency definition.
- **Migrate `bicameral-mind` and agent infra into the workspace too** — rejected for this pass: separate, much larger system (debate pipeline, k3s cluster, Discord bots); out of scope for a basic environment bootstrap migration.

## Consequences
- Dotfile Packages are versioned alongside orchestrator planning docs in one `git` history — one clone bootstraps both.
- Losing the Host Fleet model means a second physical machine will need its own bootstrap approach revisited later (no `upstream` sync mechanism carried over).
- `bicameral-mind`/agent infra remains only in the archived repo; reviving it later requires deliberately re-importing it, not automatic inheritance.
- Arch-port Makefile targets are paru-specific; switching AUR helpers later requires editing those targets directly (no abstraction layer introduced).
