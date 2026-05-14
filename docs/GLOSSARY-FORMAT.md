# GLOSSARY.md Format

## Structure

Alphabetically sorted. One entry per term.

```md
# Glossary

**Customer**:
A person or organization that places orders.
_Avoid_: client, buyer, account

**Fulfillment**:
The process of picking and shipping an order after it is placed.
_Avoid_: shipping, dispatch

**Invoice**:
A request for payment sent after delivery.
_Avoid_: bill, payment request
```

## Rules

- **Alphabetical order.** Sort entries by term name.
- **One sentence max.** Define what the term IS, not what it does.
- **`_Avoid_` line.** List aliases when alternatives exist. Omit the line if none.
- **Domain-only terms.** General programming concepts (timeouts, error types, utility patterns) don't belong even if used extensively.
- **Be opinionated.** When multiple words exist for the same concept, pick one and list the others as avoid.

## Relationship to CONTEXT.md

`GLOSSARY.md` owns all term definitions. `CONTEXT.md` holds everything else: purpose paragraph, Relationships, Example dialogue, Flagged ambiguities. Never duplicate terms between the two.

## Multi-context repos

Each bounded context gets its own `GLOSSARY.md` as a sibling to its `CONTEXT.md`:

```
src/ordering/CONTEXT.md
src/ordering/GLOSSARY.md
src/billing/CONTEXT.md
src/billing/GLOSSARY.md
```

Terms that span multiple contexts live in a root `GLOSSARY.md`. The `CONTEXT-MAP.md` references each `GLOSSARY.md` in its context listing.
