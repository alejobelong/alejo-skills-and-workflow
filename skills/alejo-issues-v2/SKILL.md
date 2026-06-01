---
name: alejo-issues-v2
description: Compact Alejo Issues v2 workflow that turns Linear PRD.xml, SAD.xml, Q&A.xml, CONTEXT.xml, prototype evidence, ADRs, review gaps, or existing Linear issues into self-contained production-ready vertical-slice Linear implementation issues with explicit providers, Doppler secret refs, XML run contracts, feature-owned code organization, and no mocks or placeholders.
---

# Alejo Issues v2

Create production-ready Linear implementation issues. Each issue must be executable by a fresh coding agent from the Linear body plus normal repo inspection.

Issues are for observable product behavior only. Planning artifacts such as `PRD.xml`, `SAD.xml`, `Q&A.xml`, `CONTEXT.xml`, `prototype.xml`, ADRs, workflow docs, and setup docs belong in Linear Project Documents, not implementation issues.

## Sources

Use canonical Linear Project Documents and current repo evidence:

1. `AGENTS.md`: project orientation and source-of-truth map.
2. `PRD.xml`: product intent, scope, user stories, and acceptance signals.
3. `SAD.xml` or `SAT.xml`: architecture, quality attributes, providers, deployment, security, operations, and code structure.
4. `Q&A.xml`: decisions, trade-offs, recommendations, and open questions.
5. `CONTEXT.xml`: domain terms, entities, relationships, and invariants.
6. `prototype.xml`: relevant UX states, flows, and visible constraints.
7. ADR XML documents: hard-to-reverse architecture decisions.
8. Existing Linear issues, comments, and Alejo Review gaps when supplied.
9. Current codebase: framework conventions, feature folders, routes, APIs, storage, tests, config, providers, and deployment.

Do not use local planning mirrors as canonical sources.

## Process

1. Resolve the Linear Project, team, issue labels/states, and writable issue destination.
2. Read the relevant Linear Project Documents, supplied issue refs, and review gaps.
3. Inspect enough code to understand existing architecture, framework constraints, test strategy, providers, env config, and feature organization.
4. Resolve unclear product, architecture, provider, dependency, or secret-name decisions before publishing. Ask concise questions with a recommended option and clear alternatives.
5. Break work into thin vertical slices: one externally observable user/operator/tester outcome per issue.
6. Publish accepted slices to Linear in dependency order, using `ready-for-agent` only when all decisions and Doppler secret names are resolved.

If Linear cannot be reached or the target project/team cannot be resolved, report the blocker and stop. Do not create local issue files.

## Issue Rules

- Each issue is self-contained: product intent, source refs, architecture constraints, domain language, providers, Doppler secret names, dependencies, preconditions, acceptance criteria, verification surface, BDD budget, and code ownership are in the XML body.
- Each issue must implement real production behavior through real UI/API/CLI/MCP surfaces, real persistence, real provider SDKs/APIs or official sandbox/test accounts, and executable tests.
- Mocks, fake providers, stubbed SDK responses, placeholder code, skipped tests, disabled branches, `NotImplemented`, TODO-only paths, and unwired UI are not valid.
- Name every provider: product, purpose, environment, integration surface, required scopes/config, and Doppler secret names.
- Reference secrets only by Doppler environment variable name. Never include secret values.
- Verify secret presence by name only when possible: `command -v doppler`, `doppler --version`, and `doppler secrets --only-names`.
- If required secrets or provider resources are missing, use `alejo-secrets`; do not mark the issue `ready-for-agent` until names exist in Doppler or the user explicitly accepts a blocked issue.
- Keep slice-owned UI, routes/API, data access, provider adapters, tests, and contracts together in the feature folder. Use framework-required route/app files only as thin adapters.
- Do not create setup-only, research-only, migration-only, adapter-only, parser-only, component-only, or route-only issues unless the user/operator/tester gets an observable outcome.

## Slice Design

Start with the smallest happy path that proves the capability end to end. Fold required schemas, migrations, validation, provider wiring, scheduled jobs, permissions, telemetry, and tests into the first slice that needs them.

Split large work by user role, scenario, state, permission boundary, data scope, integration boundary, or happy path versus important edge case. Blockers should be prior observable behavior issues or unresolved human decisions, not vague technical phases.

## Verification Contract

Each issue body, or the generated BDD budget derived from it, must include:

- Representative prompts, inputs, payloads, or user actions for the slice; chat and managed-agent work must include realistic prompts and expected answer properties.
- Playwright verification for every UI or browser-reachable surface: route/URL, user actions, visible assertions, and any persistence, network, or provider-backed evidence.
- Provider or managed-agent evidence that proves real integration, such as request IDs, trace IDs, webhook event IDs, provider sandbox records, stored records, or agent response evidence. Never include secret values.
- Latency, timeout, retry, and max-wait expectations for real-surface verification, including slow-path UX when relevant.

## Pre-Publish Gate

Before publishing, each issue must pass:

- Observable outcome is clear.
- One fresh agent can implement and verify it from the issue plus repo inspection.
- Source refs and domain terms match the Linear Project Documents.
- Providers, Doppler secret refs, preconditions, and dependencies are explicit.
- Acceptance criteria prove behavior through the declared `api`, `ui`, `cli`, or `mcp` surface.
- Representative inputs/prompts, Playwright expectations, provider/managed-agent evidence, and latency/timeout expectations are defined.
- Production constraints reject mocks, fakes, stubs, placeholders, skipped tests, disabled branches, and unwired UI.
- Code organization points to one owning feature area plus any thin framework adapters.

Show the proposed issue set before publishing with title, blockers, source refs, providers/secrets, observable outcome, surface, code organization, and why each is a vertical slice.

## Issue XML

```xml
<?xml version="1.0" encoding="UTF-8"?>
<vertical_slice_issue type="AFK" readiness="{ready-for-agent|blocked}">
  <title><![CDATA[{Short behavior-first title.}]]></title>
  <what_to_build><![CDATA[{End-to-end production behavior and externally observable outcome.}]]></what_to_build>
  <necessary_context>
    <product_intent><![CDATA[{PRD.xml requirement, user story, or review gap.}]]></product_intent>
    <architecture_constraints><![CDATA[{SAD.xml/SAT.xml, ADR, security, quality, provider, deployment, or operations constraints.}]]></architecture_constraints>
    <domain_language><![CDATA[{CONTEXT.xml and Q&A.xml terms or decisions required for this slice.}]]></domain_language>
    <prototype_evidence><![CDATA[{Relevant prototype.xml state or interaction evidence, or None.}]]></prototype_evidence>
    <source_refs><![CDATA[{Short Linear Project Document, ADR, issue, or review refs.}]]></source_refs>
  </necessary_context>
  <providers>
    <provider name="{provider or None}" purpose="{why needed}" environment="{production|sandbox|staging|local|test-account|none}" surface="{api|sdk|webhook|cli|mcp|database|queue|storage|local-service|none}">
      <credential_refs><![CDATA[{Doppler secret names only, or None.}]]></credential_refs>
      <requirements><![CDATA[{scopes, callback URLs, webhook events, models, regions, plans, permissions, or None.}]]></requirements>
    </provider>
  </providers>
  <code_organization>
    <slice_owned_folder>features/{capability-slug}/</slice_owned_folder>
    <rule><![CDATA[Keep UI, API/route handling, data access, provider adapters, tests, and contracts for this behavior colocated in the slice.]]></rule>
    <framework_mapping><![CDATA[{Thin framework adapters required elsewhere, or None.}]]></framework_mapping>
    <shared_code><![CDATA[{Cross-cutting shared modules allowed for this slice and why, or None.}]]></shared_code>
  </code_organization>
  <run_contract>
    <surface>{api|ui|cli|mcp}</surface>
    <preconditions><![CDATA[{Required state, role, data, config, provider setup, or None.}]]></preconditions>
    <dependencies><![CDATA[{Blocking issue refs, or None.}]]></dependencies>
    <secrets_refs><![CDATA[{Doppler secret names verified by name-only check, or None.}]]></secrets_refs>
    <quality_attributes><![CDATA[{Slice-relevant SAD.xml/SAT.xml quality targets.}]]></quality_attributes>
    <bdd_budget>{default 3 outer repair iterations unless SAD.xml/SAT.xml says otherwise}</bdd_budget>
    <representative_prompts><![CDATA[{Representative prompts, inputs, payloads, or user actions; required for chat/managed-agent slices, otherwise None.}]]></representative_prompts>
    <playwright_verification><![CDATA[{Required route/URL, actions, visible assertions, persistence/network/provider evidence for UI or browser-reachable surfaces, otherwise None.}]]></playwright_verification>
    <provider_managed_agent_evidence><![CDATA[{Request IDs, trace IDs, webhook event IDs, provider sandbox records, stored records, managed-agent response evidence, or None.}]]></provider_managed_agent_evidence>
    <latency_timeout_expectations><![CDATA[{Expected latency, max timeout, retry/backoff, synthetic-test wait limits, and slow-path UX if relevant.}]]></latency_timeout_expectations>
    <readiness_label_status><![CDATA[Use ready-for-agent only when decisions are resolved and required Doppler secret names exist.]]></readiness_label_status>
  </run_contract>
  <production_constraints>
    <required><![CDATA[Use real production code paths, real provider SDKs/APIs or official sandbox/test accounts, real persistence, real wiring, and executable tests.]]></required>
    <invalid><![CDATA[Mocks, fake providers, stubbed SDK responses, placeholder code, skipped tests, disabled branches, NotImplemented, TODO-only paths, and unwired UI are not accepted.]]></invalid>
  </production_constraints>
  <acceptance_criteria>
    <criterion><![CDATA[{Externally verifiable behavior works through the declared surface.}]]></criterion>
    <criterion><![CDATA[{Relevant state, storage, provider, or UI effect is real and observable.}]]></criterion>
    <criterion><![CDATA[{Security, quality, and test expectations from source docs are satisfied.}]]></criterion>
    <criterion><![CDATA[{No invalid production shortcuts remain.}]]></criterion>
  </acceptance_criteria>
  <blocked_by><![CDATA[{Blocking issue refs or unresolved decision, or None.}]]></blocked_by>
</vertical_slice_issue>
```

Keep issue bodies just sufficient. Do not paste whole planning documents, broad background, stale file guesses, implementation code, or anything an agent can discover by inspecting the repo.
