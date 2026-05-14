# Rules — git-orchestrator

Operational rules governing how AI agents interact with files, tools, and each other. Distinct from LANGUAGE.md (naming/framing) and CONTEXT.md (relationships).

## AI Agent File Ownership

- AGENTS.md is Codex-owned after first generation. holistic-ai reads but does not overwrite it on re-run.
- CLAUDE.md is holistic-ai-owned. Re-generated fresh from AGENTS.md on every holistic-ai re-run.
- GEMINI.md is Gemini-owned. Generated once by Gemini; holistic-ai does not touch it after initial generation.
- QWEN.md is Qwen-owned. Synthesized from GEMINI.md + domain docs + AGENTS.md in Traditional Chinese.
- CLAUDE.md and GEMINI.md are **never symlinks**. Always independent generated files.

## AI Agent Read Permissions

| Agent | Reads | Does not read |
|-------|-------|--------------|
| Claude (logic debater) | CLAUDE.md | GEMINI.md, QWEN.md |
| Gemini (feelings debater) | GEMINI.md | CLAUDE.md, QWEN.md |
| Codex (maintainer) | AGENTS.md | CLAUDE.md, GEMINI.md, QWEN.md |
| Qwen (observer) | QWEN.md | CLAUDE.md, GEMINI.md |
| Orchestrator (main thread) | synthesis output | individual debater files |

Epistemic separation is intentional — debaters must not see each other's context before committing their position.

## Debate Execution Rules

- Round 1 (logic + feelings) runs in parallel. No shared context between debaters before output is committed.
- Observer synthesizes after Round 1 completes — never before.
- Orchestrator concludes after observer synthesis — never before.
- Debate is triggered on demand only. holistic-ai file prep does not trigger debate.

## holistic-ai Re-run Rules

- Always regenerate: CLAUDE.md
- Never overwrite: AGENTS.md (read as source only), GEMINI.md, QWEN.md
- Always ask on conflict: existing doc language vs chosen DOC_LANGUAGE
