# ROADMAP Format

`ROADMAP.md` sits at the repo root alongside `TASKS.md`. It is the strategic complement to TASKS.md's tactical focus.

## When to offer a ROADMAP

Offer `ROADMAP.md` when any of these appear in the conversation:

- Milestones that span multiple months or multiple TASKS.md cycles
- Outcomes not tracked in the issue tracker (billing gates, contractual deadlines, relationship checkpoints, product themes)
- Stakeholder-facing goals distinct from developer work items

## Hierarchy

| Layer | File | Horizon | Focus | Audience |
|-------|------|---------|-------|----------|
| Strategic | `ROADMAP.md` | Months | Outcomes / milestones | Stakeholders + AI context |
| Tactical | `TASKS.md` | Weeks | Work items (pending) | Developer + AI agent |
| Execution | Daily Log | Days | Completed work + SHAs | Developer + AI agent |

Tasks in `TASKS.md` should map to a phase in `ROADMAP.md`. When a group of work items is complete, a milestone can be checked off. AI agents use `ROADMAP.md` to verify that current work aligns with the active phase.

## Template

```md
# Roadmap — [Project Name]

## Vision
[1-2 sentences: what does success look like at the horizon?]

## Phases

### Phase N — [Theme] (Target: [Month YYYY])
[Outcome sentence: what will be true when this phase is complete?]

Key milestones:
- [ ] Milestone A
- [ ] Milestone B

### Phase N+1 — [Theme] (Target: [Month YYYY])
[Outcome sentence.]

Key milestones:
- [ ] Milestone C

## Current Focus
→ Phase N — [what specifically is in flight right now]
```

## Notes

- Dates are targets, not commitments — use month/quarter granularity, not exact dates
- Milestones describe outcomes ("billing integration live"), not tasks ("implement Stripe")
- When a milestone completes, check it off in place — ROADMAP.md is a living document, not an append-only log (unlike ADRs)
- If a phase is deprioritised or superseded, strike it through and add a note rather than deleting it — context about dropped directions is valuable
