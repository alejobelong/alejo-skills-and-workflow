---
name: alejo-questions
description: Alejo Questions session that challenges a plan, design, architecture, feature idea, or implementation approach against the existing codebase, domain model, CONTEXT.xml glossary, ADRs, and Alejo documentation workflow. Use when the user wants to run Alejo Questions, stress-test, interrogate, refine, or sharpen a proposal through structured multiple-choice questions against the project's language and documented decisions.
---

<what-to-do>

Interview the user relentlessly about every aspect of the plan until there is a shared understanding. Walk down each branch of the design tree, resolving dependencies between decisions one by one. For each question, provide multiple-choice options, mark your recommended answer, and briefly explain why each option is viable. Number questions sequentially starting at 1.

Ask one numbered multiple-choice question at a time and wait for feedback before continuing.

If the user has not supplied a plan, proposal, or design, request it before starting the Alejo Questions session.

If a question can be answered by exploring the codebase or docs, explore first and report the evidence instead of asking the user to answer from memory.

Start a running Q&A record immediately. Use it to create the final Alejo Questions session log when the session ends or stops.

</what-to-do>

<supporting-info>

## Domain awareness

During codebase exploration, also look for existing documentation and repository instructions:

- Linear Project Documents `AGENTS.md`, `issue-tracker.md`, `triage-labels.md`, `alejo-workflow.md`, and `WORKFLOW.md`, when configured
- `CONTEXT-MAP.xml`
- root or context-local `CONTEXT.xml`
- root or context-local `docs/adr/`
- old local `AGENTS.md`, `docs/agents/`, or `WORKFLOW.md` files only as legacy mirrors, not canonical sources
- Linear Project Documents named `Q&A.xml` and `CONTEXT.xml`, when configured
- nearby source files that implement the concepts under discussion

### File structure

Most Alejo repos have a single context:

```text
/
|-- CONTEXT.xml
|-- docs/
|   `-- adr/
`-- src/
```

If a `CONTEXT-MAP.xml` exists at the root, the repo has multiple contexts. The map points to where each one lives:

```text
/
|-- CONTEXT-MAP.xml
|-- docs/
|   `-- adr/              # system-wide decisions
`-- src/
    |-- ordering/
    |   |-- CONTEXT.xml
    |   `-- docs/adr/     # context-specific decisions
    `-- billing/
        |-- CONTEXT.xml
        `-- docs/adr/
```

Create files lazily, only when there is something to write. If no `CONTEXT.xml` exists, create one when the first project-specific term is resolved. If no `docs/adr/` exists, create it when the first ADR is needed. Always create the final Alejo Questions session log at the end, even if no glossary or ADR changed. In Linear-configured repos, publish `Q&A.xml`, `CONTEXT.xml`, and any ADR documents only once, in a final session-close batch.

All generated planning artifacts from this skill must be XML. Put user-supplied prose, code snippets, quotes, and copied evidence inside CDATA sections or escape XML special characters.

## During the session

Every Alejo Questions prompt must be numbered and multiple choice. Keep options short, mark the recommended option, explain why it is recommended, explain why the other options are interesting or viable, and include an "Other / correction" option when the listed choices may not cover the user's intent.

### Clear question shape

Ask questions in plain language before naming the abstract decision. If the topic is technical, domain-specific, or policy-like, first explain what is really being decided, why it matters, and 2-4 concrete examples of moments where the choice would apply.

Use this compact shape:

```md
## Question {N}: {short plain-English title}

The real question is: {plain-English decision}.
This matters because {one concrete consequence}.
Examples: {2-4 short scenarios}.
My recommendation: {simple policy or choice}.

A. {Option} (Recommended)
{One clear sentence about what this means.}
B. {Option}
{One clear sentence about when this is viable.}
C. Other / correction
```

Avoid unexplained jargon in the question title. If a useful analogy would make the trade-off obvious, include one short analogy before the options.

### Challenge against the glossary

When the user uses a term that conflicts with the existing language in `CONTEXT.xml`, call it out immediately. Example: "Your glossary defines 'cancellation' as X, but you seem to mean Y. Which should we use? A) Existing glossary meaning (recommended, keeps language stable), B) New meaning from this plan (viable if the domain language has changed), C) Other / correction."

### Sharpen fuzzy language

When the user uses vague or overloaded terms, propose a precise canonical term. Example: "You're saying 'account'. Which term should this be? A) Customer (recommended, matches the business actor), B) User (viable if this is about authentication), C) Other / correction."

When one word names multiple concepts, separate the concepts and present the meanings as options. When multiple words name the same concept, pick one canonical term and list the others as terms to avoid.

### Discuss concrete scenarios

When domain relationships are being discussed, stress-test them with concrete scenarios. Invent edge cases that force precision around boundaries, ownership, cardinality, lifecycle, failure modes, and cross-context behavior.

### Cross-reference with code and docs

When the user states how something works, check whether the code agrees. If you find a contradiction, surface it plainly. Example: "The code cancels entire Orders, but the plan assumes partial cancellation is possible. Which source should change? A) Adjust the plan to match whole-order cancellation (recommended, smallest change), B) Change the domain to support partial cancellation (viable if the new behavior is required), C) Other / correction."

When docs contradict code, present the likely resolutions as options: documentation is stale, implementation is wrong, or the plan should be adjusted.

### Update CONTEXT.xml inline

When a project-specific term or relationship is resolved, update the relevant `CONTEXT.xml` right there. Do not batch these up. Use the format in [context-format.md](./references/context-format.md).

`CONTEXT.xml` must stay devoid of implementation details. Do not treat it as a spec, scratch pad, or repository for implementation decisions. It is a glossary and relationship map.

If the repo is configured for Linear Project Documents, do not sync `CONTEXT.xml` during the session. Add it to the final Linear publish batch with `Q&A.xml` and any ADR documents.

### Offer ADRs sparingly

Only offer to create an ADR when all three are true:

1. Hard to reverse: the cost of changing the decision later is meaningful.
2. Surprising without context: a future reader would wonder why this path was chosen.
3. Real trade-off: there were meaningful alternatives and one was selected for specific reasons.

If any of the three is missing, skip the ADR. When the decision qualifies and is settled, create or update the ADR locally using [adr-format.md](./references/adr-format.md); publish ADR documents to Linear only in the final session-close batch.

### Keep the Q&A record

For every question, record the question number, issue being tested, options given, recommended answer, rationale for the recommendation, why other options were viable, user answer, evidence checked, resolution, and docs changed. Keep the same question number in the visible prompt, running Q&A record, final session log, and Linear `Q&A.xml` document. Record only visible questions, recommendations, answers, evidence, and outcomes. Do not include hidden reasoning.

### Write the final session log

At the end of every Alejo Questions session, create an XML log using [session-log-format.md](./references/session-log-format.md).

Default path:

```text
docs/questions/YYYY-MM-DD-<topic-slug>.xml
```

If the repository has a different Alejo documentation convention, follow it while keeping the file easy to find. If the session stops early, create the log with the Q&A collected so far and mark unresolved items clearly.

Include the original plan or summary, every question asked, every recommended answer, the user's answers or corrections, evidence from code or docs, resolved terminology and relationships, ADRs created or updated, open questions, follow-ups, and unresolved contradictions.

In Linear-configured repos, publish the final log to the Linear Project document named `Q&A.xml`, publish the final `CONTEXT.xml`, and publish any ADR documents in one closing batch. If the Project already has a `Q&A.xml` document, update it in place with the latest session rather than creating a Linear issue.

</supporting-info>
