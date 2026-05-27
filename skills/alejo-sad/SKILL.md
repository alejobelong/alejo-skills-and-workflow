---
name: alejo-sad
description: Use when a user wants a SAD.xml, solution architecture document, architecture spec, technical architecture, or architecture design that explains requirements, prototype evidence, quality attributes, vertical-slice code organization, simple high-level diagrams, security, operations, and ADR-linked decisions.
---

# Alejo SAD

Create a compact Solution Architecture Document in XML. Optimize the architecture for the highest-priority quality attributes and make trade-offs explicit.

## Process

1. Use the current context window first. Then inspect relevant Linear Project Documents (`PRD.xml`, `Q&A.xml`, `CONTEXT.xml`, `prototype.xml`), local mirrors such as latest `docs/questions/` logs, prototype reports in `docs/prototypes/`, `CONTEXT.xml`/`CONTEXT-MAP.xml`, ADRs, plans, code, and other prior Alejo-skill outputs.
2. If unclear, ask exactly these initial quality-attribute questions one at a time as multiple choice. For each, put the recommended option first with a short rationale, then let the user confirm/correct:
   - Which 3 quality attributes should drive the architecture?
   - What measurable targets or constraints define success for them?
   - Which trade-offs are acceptable to improve them?
3. Draft one XML SAD. In Linear-configured repos, publish it to the Linear Project document named `SAD.xml` by default, or `SAT.xml` only when the repo/user already uses that title. A local `docs/architecture/YYYY-MM-DD-<topic>-sad.xml` file may be used as a working copy or mirror, but it is not the canonical published artifact.
4. Use Mermaid for every diagram inside XML CDATA. Keep diagrams simple, high-level, complete, and truthful to the architecture that should be implemented. Do not use image files or prose-only diagrams.
5. Use prototype evidence to inform architecture and trade-offs, but do not treat prototype code as production design unless the user explicitly approved promoting it.
6. Require vertical-slice code organization in the SAD so later `alejo-issues` slices can map each user-facing capability to one feature folder.
7. Link ADRs for major decisions; create or propose ADRs for new hard-to-reverse decisions.

## Quality Attributes

Use this checklist, then keep only relevant attributes in the SAD: performance (latency, throughput, resource use), availability/reliability/resilience, scalability/capacity/concurrency, security/privacy/compliance, maintainability/modifiability/testability, operability/observability/auditability, data integrity/consistency/durability, interoperability/compatibility, usability/accessibility, portability/deployability, cost efficiency.

## Code Organization Rule

Every SAD must prescribe production code around vertical slices/features, not horizontal technical layers. A slice is one user-facing capability folder containing its UI, API/route, data access, tests, and shared contracts together, adapted to the repo's framework.

```text
features/
  create-order/
    CreateOrderForm.tsx
    create-order.route.ts
    create-order.db.ts
    create-order.test.ts
    create-order.types.ts
```

Do not propose catch-all layer files such as `controllers/OrderController.ts`, `services/OrderService.ts`, or `repositories/OrderRepository.ts` that mix create, cancel, update, and other capabilities. Shared code is allowed only for genuinely cross-cutting or multi-slice concerns; keep it small and name why it is shared. If a framework requires conventional route/app files, document the thin adapter mapping and keep slice-owned logic, tests, and contracts colocated with the feature.

## Diagram Discipline

Every diagram should be readable in one glance and accurate enough to guide implementation.

- Prefer 5-9 meaningful nodes. Use more only when omitting a node would make the architecture untruthful.
- Show major actors, runtimes, trust boundaries, durable stores, and external integrations. Move classes, functions, files, methods, prompt steps, retry branches, labels, and per-field details into prose or tables.
- Use one edge per important relationship. Label edges only when the protocol, direction, or data contract is architecturally important.
- For components/connectors, show responsibilities and integration paths, not internal call stacks.
- For data diagrams, show durable entities and ownership boundaries, not every attribute.
- For deployment/network diagrams, show environments, runtime boundaries, public/private edges, stores, queues, and third-party systems. Avoid subnet, port, firewall, container, and job-level detail unless it is a key design decision.
- Do not invent services, networks, queues, databases, or agents just to make a diagram look complete. Mark optional or future elements explicitly, or leave them out.
- If a diagram becomes dense, replace detail with a simpler overview plus a short table of details.

## SAD Template

```xml
<?xml version="1.0" encoding="UTF-8"?>
<solution_architecture_document title="{Title}">
  <context><![CDATA[{Purpose, scope, assumptions, links to PRD/context/prototype reports/ADRs.}]]></context>
  <prototype_evidence>
    <evidence>
      <question_tested><![CDATA[{prototype question}]]></question_tested>
      <result><![CDATA[{evidence summary}]]></result>
      <architectural_impact><![CDATA[{decision, constraint, risk, or no impact}]]></architectural_impact>
    </evidence>
  </prototype_evidence>
  <functional_requirements>
    <capability><![CDATA[{Capability}]]></capability>
  </functional_requirements>
  <quality_attributes>
    <attribute name="{name}">
      <target><![CDATA[{metric/SLA/constraint}]]></target>
      <architectural_response><![CDATA[{design choice}]]></architectural_response>
      <trade_off><![CDATA[{cost/risk}]]></trade_off>
    </attribute>
  </quality_attributes>
  <architecture><![CDATA[{Short explanation of the chosen architecture and why it fits the top quality attributes.}]]></architecture>
  <code_organization>
    <description><![CDATA[{Describe how future vertical slices map to feature folders. Avoid horizontal controller/service/repository ownership.}]]></description>
    <feature_folder_example><![CDATA[
features/
  {capability-slug}/
    {Capability}View.tsx
    {capability-slug}.route.ts
    {capability-slug}.db.ts
    {capability-slug}.test.ts
    {capability-slug}.types.ts
]]></feature_folder_example>
    <shared_code><![CDATA[{Only cross-cutting or multi-slice modules, with rationale.}]]></shared_code>
    <framework_mapping><![CDATA[{If the framework requires route/app files elsewhere, explain the thin adapter to slice-owned logic.}]]></framework_mapping>
  </code_organization>
  <diagrams>
    <diagram type="components_and_connectors" language="mermaid">
      <purpose><![CDATA[{One-sentence purpose: what this diagram helps the reader understand.}]]></purpose>
      <source><![CDATA[
flowchart LR
  User --> App
  App --> Service
  Service --> DataStore[(Data Store)]
]]></source>
    </diagram>
    <diagram type="data_layer" language="mermaid">
      <purpose><![CDATA[{One-sentence purpose: what durable data relationships or ownership boundaries matter.}]]></purpose>
      <source><![CDATA[
erDiagram
  USER ||--o{ ORDER : places
]]></source>
    </diagram>
    <diagram type="deployment" language="mermaid">
      <purpose><![CDATA[{One-sentence purpose: what runtime, trust, and network boundaries matter.}]]></purpose>
      <source><![CDATA[
flowchart TB
  Internet --> LB[Load Balancer]
  LB --> App[App Runtime]
  App --> DB[(Database)]
]]></source>
    </diagram>
  </diagrams>
  <security><![CDATA[{Identity/authn/authz, secrets, encryption, network boundaries, privacy/compliance, threat assumptions.}]]></security>
  <operations><![CDATA[{Monitoring, alerting, audit logs, backup/restore, incident response, SLO/SLA expectations, runbooks.}]]></operations>
  <adr_links>
    <adr title="{ADR title}" href="{path/link}" />
  </adr_links>
  <risks_and_open_questions>
    <item><![CDATA[{Risk or question}]]></item>
  </risks_and_open_questions>
</solution_architecture_document>
```
