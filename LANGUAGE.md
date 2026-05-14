# Language — git-orchestrator

## Rejected Framings

| Use | Do not use |
|-----|-----------|
| Project | repo, app, site |
| Work Item | ticket, task, issue, card, story (unless quoting issue tracker hierarchy) |
| Daily Log | task file, daily standup, journal |
| Backlog | todo, roadmap, sprint |
| Tag | label, type, category |
| ADR | design doc, RFC |
| Sub-submodule | inner repo, nested repo |
| Issue (GitHub) | work item (reserved for external tracker), ticket, card |
| HIC | H-OFF (old name) |
| Logic Debater | Claude agent, code debater |
| Feelings Debater | Gemini agent, narrative debater |
| Maintainer | implementor, developer agent |
| Observer | watcher, monitor |
| Orchestrator (debate) | coordinator, moderator |
| AGENTS.md | AI docs, agent instructions file |
| CLAUDE.md (independent) | Claude symlink |
| GEMINI.md (independent) | Gemini symlink, documentation file |

## Behavioral Rules

### Prepare-Then-Prompt
AI never asks "Do you want to do X?" It does the prep, then states "I have completed X. Ready for your review/approval." Asking permission before acting is not permitted for `[HOOTL]` tasks unless low confidence is surfaced later.

### Actionable Context on Pause
When surfacing an `[HITLFE]` task, the AI must show: (1) what it already did, (2) why human input is needed, (3) what the potential impact is. No raw dumps — structured summary only.

### Threshold-Based Routing
AI routes to human only when confidence in outcome is low or stakes are high. Routine, reversible, well-scoped work is `[HOOTL]`.

### Daily HITL Briefing
When multiple `[HITLFE]` and `[HIC]` tasks accumulate, they are surfaced as a single grouped briefing, not scattered one-by-one.

## Resolved Ambiguities

- "task" was used to mean both an external **Work Item** and a line in the **Daily Log** — resolved: **Work Item** is the external tracker unit, **Daily Log** is the markdown record.
- "tag" was used to mean both a git tag and a line-item prefix — resolved: **Tag** always means the Conventional Commits type prefix in this context.
