---
name: alejo-prd-v2
description: Compact Alejo PRD v2 workflow that turns the latest Alejo Q&A.xml, product context, and minimal repo evidence into a product-focused PRD.xml Linear Project Document. Use when the user wants a leaner PRD skill that strongly prioritizes the Alejo Q&A log and always publishes to Linear Project Documents without PRD issues, project-overview fallbacks, or local canonical files.
---

# Alejo PRD v2

Create or update `PRD.xml` as a Linear Project Document. Do not create PRD issues, project overview fallbacks, or local canonical PRD files.

## Clarification

`PRD.xml` has one destination: the Linear Project's Project Documents. If a writable Linear Project cannot be resolved, stop and report the blocker. Do not publish to a Linear issue, do not use the project description as a substitute, and do not create a local replacement.

## Source Order

Read only what is needed, in this order:

1. `Q&A.xml`: primary source. Carry forward the latest resolved questions, recommendations, answers, product snapshot, open questions, and decisions.
2. `CONTEXT.xml`: domain glossary and relationships; use its canonical terms.
3. Current conversation: latest user intent and corrections.
4. Existing `PRD.xml`: preserve still-valid product decisions when updating.
5. `prototype.xml`: UX evidence, reference notes, and visible interaction details.
6. Code/repo evidence: current product behavior and constraints only.
7. ADR XML: product-visible constraints only; leave architecture details for SAD.

Do not load setup docs such as `AGENTS.md`, `issue-tracker.md`, `triage-labels.md`, `alejo-workflow.md`, or `WORKFLOW.md` unless needed only to locate the Linear Project.

## Process

1. Resolve exactly one Linear Project from the current context, Linear links, or available Linear tooling.
2. Read the latest `Q&A.xml` first. If it is missing, synthesize from the conversation and say the PRD has weaker product confidence.
3. Explore only enough code/docs to avoid false product claims.
4. Write a short product PRD: problem, desired experience, users, stories, acceptance signals, scope, risks/open questions.
5. Publish by creating or updating Linear Project Document `PRD.xml`.

Do not interview the user. If product intent is still unclear, publish the clearest PRD possible with explicit open questions.

## Product Rules

- Stay product-facing. No modules, APIs, schemas, tests, file paths, or implementation plans.
- Use `CONTEXT.xml` terminology.
- Treat Q&A answers as higher priority than old PRDs or guesses.
- Make lists short: 3 primary items first, then additional items only when useful.
- Use XML elements for structure and CDATA for prose, evidence, quotes, and user text.

## PRD XML

```xml
<?xml version="1.0" encoding="UTF-8"?>
<prd title="{Title}">
  <source_summary>
    <primary_source>Q&amp;A.xml</primary_source>
    <confidence>{high|medium|low}</confidence>
    <notes><![CDATA[{What the PRD is mainly based on, especially Q&A decisions.}]]></notes>
  </source_summary>
  <problem_statement><![CDATA[{User-facing problem.}]]></problem_statement>
  <desired_experience><![CDATA[{End-user experience and value proposition.}]]></desired_experience>
  <users>
    <user priority="primary" order="1"><![CDATA[{User/actor and context.}]]></user>
  </users>
  <user_stories>
    <story priority="primary" order="1">
      <actor><![CDATA[{actor}]]></actor>
      <want><![CDATA[{capability}]]></want>
      <benefit><![CDATA[{benefit}]]></benefit>
      <sentence><![CDATA[As a {actor}, I want {capability}, so that {benefit}.]]></sentence>
    </story>
  </user_stories>
  <experience_notes>
    <note priority="primary" order="1"><![CDATA[{Key user-visible behavior, state, tone, permission, or constraint.}]]></note>
  </experience_notes>
  <acceptance_signals>
    <signal priority="primary" order="1"><![CDATA[{Observable signal that the experience works.}]]></signal>
  </acceptance_signals>
  <scope>
    <in><![CDATA[{Included product behavior.}]]></in>
    <out><![CDATA[{Excluded product behavior.}]]></out>
  </scope>
  <risks_and_open_questions>
    <item><![CDATA[{Risk, unresolved question, or assumption.}]]></item>
  </risks_and_open_questions>
</prd>
```

## Output Rules

- Always publish to Linear Project Document `PRD.xml`.
- Do not create a PRD Linear issue.
- Do not use Linear project overview/description as a fallback.
- Do not create a local canonical PRD file.
- If Linear publishing is blocked, report the exact blocker and stop.
