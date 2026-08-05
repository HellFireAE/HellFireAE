# CLAUDE.md

Behavioral guidelines cut common LLM coding mistakes. Merge with project-specific instructions as needed.

**Tradeoff:** Bias toward caution over speed. Trivial tasks: use judgment.

## 1. Think Before Coding

**No assumptions. No hidden confusion. Surface tradeoffs.**

Before implementing:
- State assumptions explicitly. Uncertain → ask.
- Multiple interpretations exist → present them, don't pick silently.
- Simpler approach exists → say so. Push back when warranted.
- Unclear → stop. Name what's confusing. Ask.

## 2. Simplicity First

**Minimum code that solves problem. Nothing speculative.**

- No features beyond what was asked.
- No abstractions for single-use code.
- No unrequested "flexibility" or "configurability".
- No error handling for impossible scenarios.
- 200 lines when 50 works → rewrite.

Ask: "Would senior engineer call this overcomplicated?" Yes → simplify.

## 3. Surgical Changes

**Touch only what you must. Clean only your own mess.**

Editing existing code:
- Don't "improve" adjacent code, comments, formatting.
- Don't refactor non-broken things.
- Match existing style.
- Unrelated dead code → mention, don't delete.

When changes create orphans:
- Remove imports/variables/functions YOUR changes made unused.
- Don't remove pre-existing dead code unless asked.

Test: every changed line traces directly to user's request.

## 4. Goal-Driven Execution

**Define success criteria. Loop until verified.**

Transform tasks into verifiable goals:
- "Add validation" → "Write tests for invalid inputs, then make them pass"
- "Fix the bug" → "Write a test that reproduces it, then make it pass"
- "Refactor X" → "Ensure tests pass before and after"

Multi-step tasks → brief plan:
```
1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]
```

Strong criteria → loop independently. Weak criteria ("make it work") → constant clarification.

---

**Working if:** fewer unnecessary diff changes, fewer overwrought rewrites, clarifying questions before mistakes not after.

## 5. Keep AGENTS.md Current

After changes: update root `AGENTS.md` + `AGENTS.md` in each dir touched. Reflect new targets, removed files, changed patterns, etc.

## 6. README Is a Product Artifact

README = front door. Non-technical readers decide if worth installing. Treat like UI copy.

- Readable by non-AI users. Translate jargon ("SessionStart hook" → "auto-runs on startup").
- Install commands must be complete + accurate. One broken command loses real users.
- Preserve intentional voice/brand. Quirky style is a choice — don't normalize it.
- Benchmark/metric numbers: verify against real runs. Never invent or round. Re-run if doubt.
- Readability check before commit: would non-programmer understand + install within 60 seconds?

## 7. Git Hygiene

After work in git repo: ask user "commit, push, or both? [both]" — default both.

## 8. Home Base

`~/.hermes/workspace` (the Hermes Operator) is the default place for real work — Agencies live under its `src/`. Tasks run directly in `$HOME` outside a project dir are infra/machine-setup only (dotfiles, package installs), not project work.

<!-- OMC:START -->
<!-- OMC:VERSION:4.15.7 -->

# oh-my-claudecode - Intelligent Multi-Agent Orchestration

You are running with oh-my-claudecode (OMC), a multi-agent orchestration layer for Claude Code.
Coordinate specialized agents, tools, and skills so work is completed accurately and efficiently.

<operating_principles>
- Delegate specialized work to the most appropriate agent.
- Prefer evidence over assumptions: verify outcomes before final claims.
- Choose the lightest-weight path that preserves quality.
- Consult official docs before implementing with SDKs/frameworks/APIs.
</operating_principles>

<delegation_rules>
Delegate for: multi-file changes, refactors, debugging, reviews, planning, research, verification.
Work directly for: trivial ops, small clarifications, single commands.
Route code to `executor` (use `model=opus` for complex work). Uncertain SDK usage → `document-specialist` (repo docs first; Context Hub / `chub` when available, graceful web fallback otherwise).
</delegation_rules>

<model_routing>
`haiku` (quick lookups), `sonnet` (standard), `opus` (architecture, deep analysis).
Direct writes OK for: `~/.claude/**`, `.omc/**`, `.claude/**`, `CLAUDE.md`, `AGENTS.md`.
</model_routing>

<skills>
Invoke via `/oh-my-claudecode:<name>`. Trigger patterns auto-detect keywords.
Tier-0 workflows include `autopilot`, `ultrawork`, `ralph`, `team`, and `ralplan`.
Keyword triggers: `"autopilot"→autopilot`, `"ralph"→ralph`, `"ulw"→ultrawork`, `"ccg"→ccg`, `"ralplan"→ralplan`, `"deep interview"→deep-interview`, `"deslop"`/`"anti-slop"`→ai-slop-cleaner, `"deep-analyze"`→analysis mode, `"tdd"`→TDD mode, `"deepsearch"`→codebase search, `"ultrathink"`→deep reasoning, `"cancelomc"`→cancel.
Team orchestration is explicit via `/team`.
Detailed agent catalog, tools, team pipeline, commit protocol, and full skills registry live in the native `omc-reference` skill when skills are available, including reference for `explore`, `planner`, `architect`, `executor`, `designer`, and `writer`; this file remains sufficient without skill support.
</skills>

<verification>
Verify before claiming completion. Size appropriately: small→haiku, standard→sonnet, large/security→opus.
If verification fails, keep iterating.
</verification>

<failure_mode_guards>
User input: when clarification, preference, or approval is required and AskUserQuestion is available, use AskUserQuestion instead of ending with a prose question; ask one focused question with 2-4 options. Use prose only when AskUserQuestion is unavailable or a free-form value is required.
Session/worktree continuity: before editing after resume/compaction or inside a linked worktree, re-check `git status --short --branch`, current cwd, and relevant `.omc/state/` or `.omc/handoffs/` artifacts so work does not continue on the wrong branch or stale context.
No fake completion: TODO-style placeholder notes, `test.skip`/`.only`, stub tests, and unimplemented branches are blockers, not evidence. Before completion, inspect changed files for these patterns and either implement them or report the blocker explicitly.
</failure_mode_guards>

<execution_protocols>
Broad requests: explore first, then plan. 2+ independent tasks in parallel. `run_in_background` for builds/tests.
Keep authoring and review as separate passes: writer pass creates or revises content, reviewer/verifier pass evaluates it later in a separate lane.
Never self-approve in the same active context; use `code-reviewer` or `verifier` for the approval pass.
Before concluding: zero pending tasks, tests passing, verifier evidence collected.
</execution_protocols>

<hooks_and_context>
Hooks inject `<system-reminder>` tags. Key patterns: `hook success: Success` (proceed), `[MAGIC KEYWORD: ...]` (invoke skill), `The boulder never stops` (ralph/ultrawork active).
Persistence: `<remember>` (7 days), `<remember priority>` (permanent).
Kill switches: `DISABLE_OMC`, `OMC_SKIP_HOOKS` (comma-separated).
</hooks_and_context>

<cancellation>
`/oh-my-claudecode:cancel` ends execution modes. Cancel when done+verified or blocked. Don't cancel if work incomplete.
</cancellation>

<worktree_paths>
State root: `.omc/` by default, or `$OMC_STATE_DIR/{project-id}/` when `OMC_STATE_DIR` is set, or the parent `.omc/` when a `.omc-workspace` marker anchors a multi-repo workspace. Runtime state includes `.omc/state/`, `.omc/state/sessions/{sessionId}/`, `.omc/notepad.md`, `.omc/project-memory.json`, `.omc/plans/`, `.omc/research/`, `.omc/logs/`, `.omc/artifacts/`, `.omc/handoffs/`, and `.omc/ultragoal/`. These are ignored operational artifacts by default; `.omc/skills/**` is the intentional committable exception for project-scoped skills. In linked git worktrees, local `.omc/` state is removed with the worktree unless centralized via `OMC_STATE_DIR`.
</worktree_paths>

## Setup

Say "setup omc" or run `/oh-my-claudecode:omc-setup`.

<!-- OMC:END -->
