# CONTEXT.md Format

Use `CONTEXT.md` as a glossary for project-specific domain language.

```md
# {Context Name}

{One or two sentences explaining what this context is responsible for.}

## Language

**{Canonical Term}**: {One-sentence definition of what the term is.}
_Avoid_: {near-synonyms or ambiguous aliases}

## Relationships

- An **{Entity}** {relationship} one or more **{Other Entities}**
- A **{Thing}** belongs to exactly one **{Owner}**

## Example Dialogue

> **Developer:** "{A realistic question using the canonical terms.}"
> **Domain expert:** "{A short answer that clarifies boundaries between terms.}"

## Flagged Ambiguities

- "{ambiguous word}" was used to mean both **{Concept A}** and **{Concept B}**. Resolution: {decision}.
```

## Rules

- Pick one canonical term when multiple words compete for the same concept.
- Define what the term is, not how the code implements it.
- Keep definitions to one sentence.
- Show important relationships and cardinality when known.
- Include only domain-specific concepts, not general programming concepts.
- Group terms with subheadings only when natural clusters emerge.
- Keep stale ambiguity notes only when they help future readers avoid repeating the confusion.
- Write only settled language. Unanswered branches belong in the Q&A log, not as implied facts in `CONTEXT.md`.
- During Alejo Questions, update the local file as terms settle, but sync Linear's `CONTEXT.md` Project document only once at session close.

## Context Maps

For multi-context repos, maintain a root `CONTEXT-MAP.md` that points to each context's glossary:

```md
# Context Map

## Contexts

- [Ordering](./src/ordering/CONTEXT.md) - receives and tracks orders
- [Billing](./src/billing/CONTEXT.md) - issues invoices and records payments

## Relationships

- **Ordering -> Billing**: Ordering emits events that Billing consumes.
```
