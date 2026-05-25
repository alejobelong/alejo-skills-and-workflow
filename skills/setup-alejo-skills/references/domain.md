# Domain Docs

Alejo skills read domain documentation before asking the user or writing artifacts.

## Before Exploring

Read whichever exists and is relevant:

- Root `CONTEXT.md`, or root `CONTEXT-MAP.md` for multi-context repos.
- Root `docs/adr/`.
- Context-local `CONTEXT.md` and `docs/adr/`.
- Prior Alejo outputs linked from `docs/agents/alejo-workflow.md`.

If files do not exist, proceed silently. `alejo-questions` creates or updates `CONTEXT.md`, `docs/adr/`, and session logs lazily when terms or decisions are resolved.

## Vocabulary

Use `CONTEXT.md` as the glossary for issue titles, PRDs, SADs, tests, and implementation names. If an output contradicts an ADR, surface the conflict explicitly.
