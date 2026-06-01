---
name: alejo-consistency-propagation-v2
description: Compact Alejo Consistency Propagation v2 workflow for reconciling Linear Project Documents, ADR XML, vertical-slice Linear issues, Doppler secret names, provider resources, review gaps, and current repo evidence after Q&A.xml, CONTEXT.xml, PRD.xml, prototype.xml, SAD.xml/SAT.xml, issue, secret, provider, or implementation changes. Use when the user wants the Alejo v2 planning stack checked, differences classified, and approved updates propagated without local mirrors.
---

# Alejo Consistency Propagation v2

Keep the Alejo v2 stack consistent. Find drift, classify it, ask one decision at a time, and apply only approved changes to the canonical Linear Project Documents, Linear issues, ADR XML documents, or Doppler name references.

Do not create local canonical files or local mirrors. Repo code is evidence; Linear Project Documents and Linear issues are the planning source of truth.

## Sources

Read only what is needed for the affected chain, but read every selected document line by line before analysis:

1. Current request, changed artifact, and `AGENTS.md` source-of-truth map.
2. `Q&A.xml`: resolved questions, recommendations, answers, product snapshot, decisions, and open questions.
3. `CONTEXT.xml`: canonical domain terms, entities, relationships, and invariants.
4. `PRD.xml`: user-facing problem, value proposition, users, scope, stories, and acceptance signals.
5. `prototype.xml`: UX states, flows, visible constraints, reference evidence, and open UX questions.
6. `SAD.xml` or `SAT.xml`: quality attributes, architecture, providers, deployment, data, security, operations, code structure, and ADR links.
7. ADR XML documents: accepted or proposed hard-to-reverse decisions.
8. Linear implementation issues: vertical-slice contracts, providers, Doppler names, verification contract, readiness, dependencies, and acceptance criteria.
9. Doppler name-only checks and provider metadata from `alejo-secrets-v2`.
10. Current repo evidence: implemented behavior, framework constraints, provider adapters, env config, tests, deployment, and verification results.
11. Operational Linear docs such as `issue-tracker.md`, `triage-labels.md`, `alejo-workflow.md`, and `WORKFLOW.md` only when issue states, labels, or Symphony execution drift is in scope.

Do not use local planning mirrors as canonical sources.

## Artifact Ownership

- `Q&A.xml`: questions, recommendations, user answers, resolved decisions, uncertainty, and product snapshot.
- `CONTEXT.xml`: stable domain glossary and relationships only.
- `PRD.xml`: product-facing experience, users, scope, stories, and acceptance signals.
- `prototype.xml`: UX evidence, states, interactions, visual constraints, and prototype-derived questions.
- `SAD.xml`/`SAT.xml`: architecture, quality attributes, providers, deployment, data, security, operations, ADR links, and feature-based code structure.
- ADR XML: durable architecture decisions with alternatives and consequences.
- Linear issues: production-ready vertical slices with self-contained XML run contracts.
- Doppler: secret names only; never secret values.
- Repo code: implementation evidence, not a replacement for planning artifacts.

## Process

1. Resolve the Linear Project, relevant Project Documents, Linear team/issues, and the changed source. If the writable Linear destination cannot be resolved, stop and report the blocker.
2. Select the smallest affected chain. Example: a provider change usually touches SAD, issues, Doppler names, and run readiness; a product decision usually touches Q&A, CONTEXT, PRD, SAD, and issues.
3. Read every selected document line by line, in document order, before extracting claims or looking for inconsistencies. Do not rely on snippets, headings, search hits, summaries, memory, or prior runs as a substitute for this reading pass.
4. Extract claims: domain terms, product behavior, scope, UX states, architecture decisions, quality attributes, providers, deployment, security, operations, ADR constraints, Doppler names, issue coverage, verification contract, dependencies, readiness, and code evidence.
5. Classify each difference before editing:
   - `missing-downstream`: accepted upstream claim is absent where it belongs.
   - `stale-downstream`: downstream artifact still says an older version.
   - `contradiction`: two sources cannot both be true.
   - `removal`: a new change removes, weakens, or narrows accepted behavior.
   - `out-of-place`: true information lives in the wrong artifact.
   - `coverage-gap`: PRD/SAD/prototype/review claim lacks a vertical-slice issue.
   - `secret-provider-drift`: provider resources or Doppler names differ across SAD/issues/Doppler.
   - `code-doc-drift`: repo behavior contradicts or exceeds the planning stack.
   - `ignore`: no propagation is needed.
6. Ask one decision at a time with a recommendation and clear alternatives. For purely mechanical propagation explicitly requested by the user, apply it directly and summarize it.
7. Apply approved changes narrowly. Use the relevant v2 skill when a substantial artifact needs regeneration: `alejo-prd-v2`, `alejo-sad-v2`, `alejo-issues-v2`, or `alejo-secrets-v2`.
8. Validate touched XML, preserve CDATA for prose/evidence, never expose secret values, and keep local mirrors untouched.
9. Finish with applied changes, deferred differences, unresolved blockers, and suggested next skill if more work remains.

## Decision Shape

```md
Difference {N}: {classification}

What changed: {short statement}
Evidence:
- {source}: {claim}
- {destination or conflicting source}: {claim or gap}

Recommendation: {action and why}

A. {recommended action} (Recommended)
B. Leave unchanged
C. Apply a narrower correction
D. Other / correction
```

Ask before removals, contradictions, provider choices, secret-name changes, readiness changes, and any update that changes product or architecture meaning.

## Propagation Rules

- Q&A decisions flow into CONTEXT, PRD, SAD, ADRs, and issues only at the right abstraction level.
- CONTEXT terms flow into PRD, SAD, issues, and review language; do not turn CONTEXT into a spec.
- PRD changes flow into prototype questions, SAD constraints, and vertical-slice issue coverage.
- Prototype evidence flows into PRD experience notes, SAD UX/architecture impacts, and issue verification expectations.
- SAD changes flow into issues, provider/Doppler requirements, deployment expectations, security/ops checks, and ADR links.
- ADR changes flow into SAD and affected issues.
- Issue changes that reveal missing product or architecture decisions flow back to Q&A/PRD/SAD before implementation.
- Secret/provider changes flow to SAD provider sections, issue provider blocks, issue `secrets_refs`, and Alejo Run readiness.
- Review gaps become issue updates or new vertical-slice issues; do not create horizontal backlog items.
- Code evidence can prove implementation gaps or stale docs, but do not rewrite product intent to match code unless the user chooses that resolution.

## Output Rules

- Do not write local planning files.
- Do not create planning issues.
- Do not publish to project descriptions as a fallback.
- Do not include secret values or commands that print them.
- Do not batch unrelated decisions into one question.
- Do not create horizontal setup, migration, adapter, parser, or test-only issues; use behavior-first vertical slices.
- Do not change code unless the user explicitly asks for implementation work.
- Keep summaries short and list exactly what changed, what was deferred, and what is blocked.
