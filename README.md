# git-orchestrator

A personal environment orchestrator. Manages project submodules, tracks daily work against an issue tracker, and records architectural decisions in one place.

## What this is

An orchestrator repo sits above your projects. It owns planning infrastructure — daily logs, ADRs, backlog — while each project lives as a git submodule with its own git history, branch strategy, and deployment pipeline.

## Structure

```
git-orchestrator/
├── docs/
│   ├── adr/                  # Architectural decision records
│   └── tasks/                # Daily work logs (YYYY-MM-DD.md)
├── src/
│   └── <repo-name>/          # Project submodules
├── TASKS.md                  # Forward-looking backlog
├── CONTEXT-MAP.md            # Context boundaries and relationships
├── GLOSSARY.md               # Canonical term definitions
├── LANGUAGE.md               # Rejected framings and behavioral rules
├── CONTEXT.md                # Relationships, examples, HITL framework
└── AGENTS.md                 # AI navigation index
```

## Getting started

1. Clone or copy this repo
2. Update `AGENTS.md`, `CONTEXT.md`, `CONTEXT-MAP.md`, `GLOSSARY.md` with your project details
3. Add a project: `git submodule add <remote-url> src/<repo-name>`
4. Run `/link-ai-agents` in Claude Code to sync AI context files
5. Copy `docs/tasks/YYYY-MM-DD.md` to today's date and start logging

## Daily workflow

1. Copy `docs/tasks/YYYY-MM-DD.md` template → today's date
2. Pull work items from your issue tracker into the daily log
3. Work → commit: `tag: Description`
4. Mark tasks complete, add commit SHA inline

## Commit format

```
feat: Add dark mode toggle
fix: Correct off-by-one in pagination
chore: Update .gitignore
```

Tags: `feat` `fix` `bug` `chore` `docs` `style` `refactor` `perf` `test` `infra`

## Adding a project

```bash
git submodule add <remote-url> src/<repo-name>
```

Then run `/link-ai-agents` in Claude Code to sync AI context files across all directories.
