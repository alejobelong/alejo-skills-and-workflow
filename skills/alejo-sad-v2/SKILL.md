---
name: alejo-sad-v2
description: Compact Alejo SAD v2 workflow that creates or updates a production-focused SAD.xml Linear Project Document from Linear PRD.xml, Q&A.xml, CONTEXT.xml, prototype evidence, ADRs, and current codebase architecture. Use when the user wants a clean solution architecture document with quality attributes, three core diagrams, providers, deployment, security, operations, and feature-based code organization.
---

# Alejo SAD v2

Create or update `SAD.xml` as a Linear Project Document. Do not create local canonical files, local mirrors, planning issues, or project-description substitutes.

## Sources

Use Linear Project Documents and current repo evidence only:

1. `PRD.xml`: product goals, scope, users, and acceptance signals.
2. `prototype.xml`: UX states, interaction evidence, and visible constraints when present.
3. `Q&A.xml`: decisions, trade-offs, recommendations, and open questions.
4. `CONTEXT.xml`: domain language, entities, relationships, and invariants.
5. ADR XML documents: existing hard-to-reverse architecture decisions.
6. Current codebase: frameworks, entry points, data stores, integrations, deployment config, tests, and existing architecture.
7. Existing `SAD.xml`: preserve still-valid architecture when updating.

Do not load local planning mirrors or workflow docs such as `issue-tracker.md`, `triage-labels.md`, `alejo-workflow.md`, or `WORKFLOW.md`.

## Process

1. Resolve the writable Linear Project and its Project Documents.
2. Read the source documents in order, then inspect only enough code to understand the actual architecture and constraints.
3. Ask one open-ended question about which quality attributes the user wants prioritized. Then propose a recommended top 3 plus a few evidence-based alternatives, and use the user's decision as the final priorities.
4. Before finalizing providers, ask concise open-ended provider questions with an AI recommendation for each unclear provider area; then design the architecture around production behavior, real providers, deployable services, durable data, and feature-based code organization.
5. Publish by creating or updating the Linear Project Document named `SAD.xml`.

If the Linear Project Document cannot be reached, report the blocker and stop.

## Content Rules

- Keep the SAD compact, implementation-guiding, and traceable to PRD/Q&A/CONTEXT/prototype/ADR evidence.
- Include exactly three main diagrams: components/connectors, data, and deployment.
- Use Mermaid inside XML CDATA for diagrams; keep them high-level and truthful.
- Name providers for every external service, runtime, data store, queue, model, payment system, email/SMS provider, storage provider, analytics tool, and auth provider.
- Prescribe feature-based code organization: each user-facing capability owns its UI, route/API, data access, tests, and contracts in one feature folder.
- Allow shared code only for real cross-cutting concerns, with a reason.
- Link existing ADRs and propose ADRs for new hard-to-reverse decisions.

## SAD XML

```xml
<?xml version="1.0" encoding="UTF-8"?>
<solution_architecture_document title="{Title}">
  <source_summary>
    <prd><![CDATA[{PRD.xml evidence used.}]]></prd>
    <prototype><![CDATA[{prototype.xml evidence used, or none.}]]></prototype>
    <q_and_a><![CDATA[{Q&A.xml decisions used.}]]></q_and_a>
    <context><![CDATA[{CONTEXT.xml terms and invariants used.}]]></context>
    <codebase><![CDATA[{Current architecture evidence inspected.}]]></codebase>
  </source_summary>
  <architecture_goal><![CDATA[{Short statement of the architecture and why it fits the product.}]]></architecture_goal>
  <quality_attributes>
    <attribute priority="1" name="{quality}">
      <target><![CDATA[{Measurable target or constraint.}]]></target>
      <response><![CDATA[{Architecture choice that supports it.}]]></response>
      <trade_off><![CDATA[{Cost, complexity, or product trade-off.}]]></trade_off>
    </attribute>
  </quality_attributes>
  <components_and_connectors>
    <summary><![CDATA[{Main runtimes, responsibilities, and integration paths.}]]></summary>
    <diagram language="mermaid"><![CDATA[
flowchart LR
  User[User] --> App[Application]
  App --> API[API or Server Actions]
  API --> Store[(Durable Store)]
  API --> Provider[External Provider]
]]></diagram>
  </components_and_connectors>
  <data_architecture>
    <summary><![CDATA[{Primary data stored, ownership, consistency, retention, and why it matters.}]]></summary>
    <diagram language="mermaid"><![CDATA[
erDiagram
  USER ||--o{ RECORD : owns
]]></diagram>
  </data_architecture>
  <deployment_and_providers>
    <summary><![CDATA[{Where the system runs, what services are deployed, and what providers are used.}]]></summary>
    <provider name="{provider}" purpose="{purpose}">
      <resource><![CDATA[{Existing or required provider resource.}]]></resource>
      <secrets><![CDATA[{Required Doppler-managed environment variables, or none.}]]></secrets>
    </provider>
    <diagram language="mermaid"><![CDATA[
flowchart TB
  Internet[Internet] --> Runtime[App Runtime]
  Runtime --> Database[(Database)]
  Runtime --> Provider[Provider Service]
]]></diagram>
  </deployment_and_providers>
  <code_structure>
    <rule><![CDATA[Organize production code by vertical feature slice, not by horizontal controller/service/repository layers.]]></rule>
    <example><![CDATA[
features/
  {capability-slug}/
    {Capability}View.tsx
    {capability-slug}.route.ts
    {capability-slug}.db.ts
    {capability-slug}.test.ts
    {capability-slug}.types.ts
]]></example>
    <framework_mapping><![CDATA[{Thin adapters required by the framework, with slice-owned logic kept in feature folders.}]]></framework_mapping>
    <shared_code><![CDATA[{Shared modules allowed only for cross-cutting concerns and why.}]]></shared_code>
  </code_structure>
  <security><![CDATA[{Authn/authz, secrets, encryption, privacy, trust boundaries, abuse cases, and compliance needs.}]]></security>
  <operations><![CDATA[{Observability, alerts, logs, audit trails, backups, migrations, runbooks, and incident handling.}]]></operations>
  <adr_links>
    <adr title="{ADR title}" href="{Linear Project Document or repo link}" status="{accepted|proposed|superseded}" />
  </adr_links>
  <risks_and_open_questions>
    <item><![CDATA[{Risk, assumption, missing provider decision, or open architecture question.}]]></item>
  </risks_and_open_questions>
</solution_architecture_document>
```
