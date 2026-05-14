# git-orchestrator

Personal environment orchestrator. Manages project submodules, tracks daily work against an issue tracker, and records architectural decisions.

## Tags

Standard tags for Daily Log line items and commit message types:

| Tag | Purpose | Example |
|-----|---------|---------|
| `feat` | New feature or functionality | Add dark mode toggle to navigation |
| `fix` | Repair a bug or error | Correct off-by-one error in pagination |
| `bug` | Synonym for Fix; use when emphasising a defect | Patch memory leak in event listener teardown |
| `chore` | Routine maintenance with no code impact | Update .gitignore to exclude build artifacts |
| `docs` | Documentation only | Update README with local setup instructions |
| `style` | Formatting with no logic change | Normalise indentation across stylesheet |
| `refactor` | Restructure without fixing or adding | Extract authentication logic into dedicated module |
| `perf` | Performance improvement | Replace synchronous file reads with async equivalents |
| `test` | Add or correct tests | Add unit tests for form validation edge cases |
| `infra` | Infrastructure or DevOps config | Update GitHub Actions Node version to 20 |

## Relationships

- A **Project** is mounted under `src/<repo-name>` and has its own git history and branch strategy
- A **Sub-submodule** lives inside a Project and has its own remote, branch rules, and PR workflow (see ADR 0005)
- A **Work Item** appears in the **Daily Log** when work is in-progress or complete
- A **Work Item** appears in the **Backlog** when planned but not yet started
- Each line item in a **Daily Log** carries a **Tag** that becomes the commit type
- An **ADR** covers orchestrator-level decisions only; project-level decisions live in `src/<repo-name>/docs/adr/`
- **ARCHITECTURE.md** is the living structural map; ADRs are the immutable log of why it got there
- An **Issue** on the orchestrator's GitHub repo is the preferred AI-automation surface; the external issue tracker remains source of truth

## Example

Seeding today's Daily Log from the template, completing a work item, and committing:

```markdown
# YYYY-MM-DD

## your-username/your-project

### [PROJ-42] Example Work Item Title

- [x] feat: Add feature A `a3f9c12`
- [x] fix: Correct edge case in B `b7e2d45`
- [ ] chore: Clean up legacy code
```

Commit for the completed items:
```
feat: Add feature A
```

## AI Agent File Relationships

- **holistic-ai** generates **AGENTS.md** (first run only) → **Codex** reads and writes implementation notes to **AGENTS.md**
- **holistic-ai** generates **CLAUDE.md** as a copy of **AGENTS.md** → refreshed on every holistic-ai re-run
- **Gemini** generates **GEMINI.md** from **AGENTS.md** + all domain docs → documentation-grade prose, never overwritten by holistic-ai
- **QWEN.md** synthesizes **GEMINI.md** + domain docs + **AGENTS.md** (Codex notes) → Traditional Chinese, read by Qwen (observer)
- **Main Claude thread** orchestrates the debate; each debater reads only its designated file — no shared context between debaters

### Debate Flow

```
holistic-ai (file prep) → [AGENTS.md | CLAUDE.md | GEMINI.md | QWEN.md]
                                                 ↓
                         /debate trigger (on demand)
                                                 ↓
            Claude (logic, reads CLAUDE.md) ──┐
            Gemini (feelings, reads GEMINI.md) ┤ → parallel
                                               ↓
                         Qwen (observer, reads QWEN.md) → synthesizes
                                               ↓
                         Orchestrator (main Claude thread) → concludes
```

### Role → Provider Mapping

| Role | Default provider | File | Replaceable by |
|------|-----------------|------|---------------|
| Logic Debater | Claude | CLAUDE.md | Local model (hardest) |
| Feelings Debater | Gemini | GEMINI.md | Local model |
| Maintainer | Codex | AGENTS.md | Local model |
| Observer | Qwen | QWEN.md | Local model |
| Orchestrator | Claude (main thread) | — | Hardest to replace |

## HITL Task Classification

AI agents classify every task node into one of three types before acting:

| Type | Name | Meaning |
|------|------|---------|
| `[HOOTL]` | Autonomous | High confidence, deterministic outcome. AI executes without prompting. |
| `[HITLFE]` | Human Required | AI does all prep work, then pauses for human approval before proceeding. |
| `[HIC]` | Human Offloaded | Task requires human creativity, judgment, or empathy. AI surfaces the task and waits. |

### Human Oversight Spectrum

| Model | Role of Human | Speed | Risk | Use Case |
|-------|--------------|-------|------|----------|
| **HITL** | Active reviewer | Slower | Low | High-stakes, high-nuance (e.g., medical, legal, architectural decisions) |
| **HOTL** | Supervisor | Fast | Medium | Real-time monitoring (e.g., customer support, content moderation) |
| **HOOTL** | Auditor (after-the-fact) | Fastest | High | High-volume, low-risk (e.g., spam filtering, log classification) |

This repo operates primarily in **HITL** mode for consequential decisions and **HOOTL** mode for routine automation. `[HITLFE]` is the explicit HITL gate; `[HIC]` is a human-only lane where AI does not attempt the task at all.
