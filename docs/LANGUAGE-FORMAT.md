# LANGUAGE.md Format

Term definitions and aliases live in `GLOSSARY.md`. `LANGUAGE.md` captures rules that aren't tied to a single term: rejected framings, cross-cutting principles, phrasing preferences that apply across the project.

Create this file lazily — only when a rule emerges that can't be expressed as a `_Avoid_` line in `GLOSSARY.md`.

## Structure

```md
# Language

{One sentence: what this language guide covers and why it exists.}

## Principles

- **{Rule name}**: {one-sentence rule — prescriptive, no hedging}

## Rejected framings

- **"{rejected term or framing}"**: {why not, and what to use instead}
```

## Trigger conditions

Create or add to `LANGUAGE.md` when any of these emerge during a session:

1. **Rejected framing** — a way of thinking about a concept that sounds plausible but leads to wrong decisions ("don't think of an Order as a shopping cart — Orders are immutable once placed")
2. **Cross-cutting principle** — a rule that governs how the project communicates across many terms ("describe behavior from the user's perspective, not the implementation layer")
3. **Phrasing preference** — a word or phrase to prefer or avoid that isn't a term alias ("use 'select' not 'click' in user stories")

## Rules

- **Principles are prescriptive.** Write them as imperatives: "Describe X as Y" not "X could be described as Y."
- **Rejected framings explain why.** The value isn't the rule — it's the reason. A reader who understands why won't need to look it up.
- **No term definitions here.** Those belong in `GLOSSARY.md`. If you find yourself defining a term, move it there.
- **Keep it short.** Three principles and two rejected framings is a healthy `LANGUAGE.md`. Ten of each is a red flag that GLOSSARY.md isn't pulling its weight.

## Multi-context repos

Each bounded context gets its own `LANGUAGE.md` as a sibling to its `CONTEXT.md` and `GLOSSARY.md`. Cross-cutting language rules live in a root `LANGUAGE.md`.
