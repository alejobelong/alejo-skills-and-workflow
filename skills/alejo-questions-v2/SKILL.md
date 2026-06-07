---
name: alejo-questions-v2
description: Compact Alejo Questions v2 session for sharpening a product idea, plan, UX, architecture, or implementation approach through evidence-first, numbered multiple-choice questions. Use when the user wants a leaner Alejo Questions workflow that drives toward a clear end-user experience, value proposition, domain language, decisions, and XML Linear Project Documents without changing the original alejo-questions skill.
---

# Alejo Questions v2

Interrogate relentlessly about every aspect of the proposal by walking down each branch of the design tree. Resolve dependencies between decisions one by one until the product experience, end-user value proposition, domain language, and important decisions are clear enough for PRD/SAD/issues. Keep it compact, evidence-first, and one question at a time.

## Rules

- If no proposal exists, ask for it before starting.
- Explore code, docs, and Linear Project Documents before asking anything the repo can answer.
- Ask exactly one visible question at a time.
- Number questions sequentially from 1; use the same number in the prompt, notes, and final XML.
- Every question is multiple choice, includes a recommended option first, and ends with `Other / correction`.
- Product clarity comes first. Ask whether to continue into technical decisions only after the experience and value proposition are clear.
- Keep `Q&A.xml` and `CONTEXT.xml` as live running artifacts from the first answered question.
- Use XML for generated artifacts. Put user prose, quotes, snippets, and evidence in CDATA.
- In Linear-configured repos, publish `Q&A.xml` and any changed `CONTEXT.xml` incrementally after each answer before asking the next question. Publish any ADR XML when created. Do not create Linear issues.

## Domain Awareness

Read only what is needed. Know what each artifact is for:

- `AGENTS.md`: repo onboarding and Alejo source-of-truth map.
- `issue-tracker.md`: Linear Project, issue contract, and Symphony handoff.
- `triage-labels.md`: Linear status and label vocabulary.
- `alejo-workflow.md`: how Alejo planning moves toward implementation.
- `WORKFLOW.md`: Symphony execution contract for ready issues.
- `Q&A.xml`: prior questions, recommendations, answers, and decisions; this skill updates it.
- `CONTEXT.xml`: domain glossary and relationships; this skill updates settled terms.
- `CONTEXT-MAP.xml`: map for repos with multiple domain contexts.
- `PRD.xml`, `prototype.xml`, `SAD.xml`/`SAT.xml`: product intent, UX evidence, and architecture constraints to respect.
- `docs/adr/*.xml`: durable architecture decisions; this skill creates one only when the decision deserves it.
- Source files: ground truth for implemented behavior and contradictions.

Legacy local `AGENTS.md`, `docs/agents/*`, or `WORKFLOW.md` are mirrors only; Linear Project Documents are canonical when configured.

## Loop

1. Summarize the proposal in one or two sentences.
2. Identify the next highest-risk ambiguity: user, job-to-be-done, promise, scope, term, state, permission, edge case, dependency, constraint, contradiction, or technical decision.
3. If evidence can answer it, inspect first and cite the evidence.
4. Ask one numbered multiple-choice question.
5. Record the answer, recommendation, evidence, resolution, and docs changed.
6. Immediately update the live `Q&A.xml`. If the answer settles a domain term, relationship, actor, capability name, state, invariant, or boundary, update `CONTEXT.xml` before asking the next question. In Linear-configured repos, publish both changed Project Documents immediately.
7. Create an ADR only when the decision is costly to reverse, surprising without context, and has real alternatives.
8. Continue until the product snapshot is clear or the user stops. Then offer a technical-decision branch.

## Question Shape

```md
## Question {N}: {plain title}

Full question: {plain-English decision}.
This matters because: {one concrete consequence}.
Evidence: {code/doc finding, or "Not checked; this needs user judgment."}
My recommendation: {recommended option and why}.

A. {Recommended option} (Recommended)
{One sentence on impact.}
B. {Alternative}
{One sentence on tradeoff.}
C. Other / correction
```

Use concrete scenarios when needed. Challenge vague or conflicting terms immediately: pick a canonical term, split overloaded terms, or ask which definition wins.

## Final XML

At session close, make one final pass over the live XML logs. If the session stops early, mark open items clearly.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<alejo_questions_v2 topic="{Topic}" status="{complete|stopped_early|blocked}">
  <product_snapshot>
    <end_user><![CDATA[{who this is for}]]></end_user>
    <value_proposition><![CDATA[{clear user value}]]></value_proposition>
    <experience><![CDATA[{what the user experiences}]]></experience>
    <scope><![CDATA[{in/out boundaries}]]></scope>
  </product_snapshot>
  <questions>
    <qa number="{N}">
      <question><![CDATA[{visible question}]]></question>
      <recommendation><![CDATA[{recommended option}]]></recommendation>
      <answer><![CDATA[{user answer or correction}]]></answer>
      <evidence><![CDATA[{code/docs checked, or None}]]></evidence>
      <resolution><![CDATA[{settled point or open contradiction}]]></resolution>
    </qa>
  </questions>
  <resolved_language>
    <term canonical="{Term}"><![CDATA[{definition or relationship}]]></term>
  </resolved_language>
  <decisions>
    <decision adr="{ADR path or Linear doc URL if any}"><![CDATA[{decision}]]></decision>
  </decisions>
  <open_questions>
    <open_question><![CDATA[{remaining ambiguity and next step}]]></open_question>
  </open_questions>
  <follow_ups>
    <follow_up><![CDATA[{PRD/SAD/prototype/issue/doc action}]]></follow_up>
  </follow_ups>
</alejo_questions_v2>
```

## Output Rules

- Do not include hidden reasoning.
- Do not ask unnumbered questions during the session.
- Do not batch multiple decisions into one question.
- Do not turn `CONTEXT.xml` into a spec; it is only glossary and relationships.
- Do not wait until session close to publish settled `CONTEXT.xml` changes in Linear-configured repos.
- Do not create ADRs for obvious, reversible, or no-tradeoff choices.
- Do not publish planning output as Linear issues.
