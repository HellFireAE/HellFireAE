<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-04-28 | Updated: 2026-04-30 -->

# git

## Purpose
Stow package for git configuration. Files mirror `$HOME` layout — stow symlinks them into `~`.

## Key Files

| File | Description |
|------|-------------|
| `.gitconfig` | Global git config: credentials, user, GPG signing, SSH — **gitignored, local only** |
| `.gitconfig.example` | Template for new devs — copy to `.gitconfig` and fill personal values |

## For AI Agents

### Working In This Directory
- `.gitconfig` is gitignored — never committed; contains personal identity, signing key, Windows paths
- `.gitconfig.example` is tracked — template only, no personal values
- `make link` copies `.gitconfig.example` → `.gitconfig` if absent, then stows
- Layout mirrors `$HOME` exactly — `.gitconfig` here → `~/.gitconfig`
- Credential helpers use `gh auth git-credential` for github.com and gist.github.com
- Commits signed via SSH key; signing program is `/opt/1Password/op-ssh-sign` (native 1Password Linux app)
- `core.sshCommand` points at the native 1Password SSH agent socket (`~/.1password/agent.sock`)
- Add new config files at same relative path they'd live under `$HOME`

### Testing Requirements
- `stow -d ~/.hermes/workspace/config -t ~ git --simulate` — dry-run, confirm no conflicts
- `git config --list --show-origin` — verify symlinked config loads correctly

### Common Patterns
- Double `helper =` lines: first clears any system-level helper, second sets the new one

## Dependencies

### External
- `gh` — GitHub CLI, provides `gh auth git-credential`
- `/opt/1Password/op-ssh-sign` — native 1Password SSH signing agent (Linux)

<!-- MANUAL: -->
