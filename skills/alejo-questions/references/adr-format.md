# ADR Format

ADRs live in `docs/adr/` unless a context-local ADR directory already exists. Use sequential numbering:

```text
0001-short-slug.md
0002-short-slug.md
```

## Minimal Template

```md
# {Short Decision Title}

{One to three sentences explaining the context, the decision, and why this decision was chosen.}
```

That is enough for most ADRs. Add sections only when they preserve useful context.

## Optional Sections

```md
---
status: accepted
---

## Considered Options

- {Option A}
- {Option B}

## Consequences

- {Non-obvious consequence}
```

## When To Create One

Create an ADR only when all three conditions hold:

- The decision would be costly to reverse.
- The choice would surprise a future reader without context.
- The team chose between real alternatives with meaningful trade-offs.

Good ADR subjects include architecture boundaries, cross-context integration patterns, lock-in technology choices, deliberate deviations from common practice, and constraints invisible in the code.

When an ADR comes from Alejo Questions, create or update it only after every question that could change the decision has been answered, explicitly deferred, or marked unresolved. Keep the ADR short and point readers to the Q&A log when the trade-off history needs more detail.
