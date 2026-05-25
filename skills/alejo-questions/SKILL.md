---
name: alejo-questions
description: Goal-driven Alejo Questions session that clarifies the product experience, end-user value proposition, domain language, and optional technical decisions before PRD/SAD/issues. Use when the user wants to sharpen a product idea, plan, design, architecture proposal, or implementation approach through structured multiple-choice questions.
---

<what-to-do>

Use Codex's native Goal flow when the session is started that way. In Codex, Goal is a composer mode and `/goal` slash command, not a callable model tool. Launch/default prompts for this skill should start with `/goal` so Codex records the session as a thread goal before the model turn begins.

Do not invent a `set_goal` tool call, `::goal` directive, or hidden action. If the invoking message is already marked as a Goal, treat that native thread goal as controlling. If the skill is not running as a native Goal, do not fail or ask the user to restart; state the goal visibly and run the same goal loop in the conversation.

Goal:

```text
Build a very clear picture of the product experience and the value proposition being built for the end user.
```

Interview the user until the goal is achieved. The product clarity goal is achieved only when these are clear enough for PRD:

- Target user and context.
- End-user pain, desire, or job to be done.
- Value proposition and promised outcome.
- Desired experience or core journey.
- Primary scenarios and success signals.
- Main scope boundaries.
- Domain terms that must be used consistently.
- Open product risks or unanswered questions.

Maintain an explicit question queue for the product clarity goal. After each answer, record the resolution, apply any local doc updates, and immediately ask the next highest-priority unanswered multiple-choice question. Do not wait for the user to say "continue" while unanswered product clarity questions remain.

Ask one multiple-choice question at a time and wait for feedback before asking the next question. For each question, mark your recommended answer and briefly explain why each option is viable.

After the product clarity goal is achieved, ask whether to continue into technical decisions:

```text
Do you want to go through technical decisions now?
A. No, stop here and publish the product Q&A (Recommended if this is headed to PRD next)
B. Yes, continue into technical decisions (Useful before SAD or issue slicing)
C. Other / correction
```

Only ask technical decision questions if the user chooses yes. Technical questions can cover architecture constraints, data shape, integration boundaries, quality attributes, implementation risks, rollout, and verification. If the user chooses yes, create a compact technical question queue and keep asking until it is exhausted or the user explicitly stops.

If the user has not supplied a plan, proposal, or design, request it before starting the Alejo Questions session.

If a question can be answered by exploring the codebase or docs, explore first and report the evidence instead of asking the user to answer from memory.

Start a running Q&A record immediately. Use it to create the final Alejo Questions session log when the session ends, when every active question queue is exhausted, or when the user explicitly stops.

</what-to-do>

<supporting-info>

## Domain awareness

During codebase exploration, also look for existing documentation and repository instructions:

- `AGENTS.md`
- `CONTEXT-MAP.md`
- root or context-local `CONTEXT.md`
- root or context-local `docs/adr/`
- `docs/agents/` workflow notes, when present
- Linear Project Documents named `Q&A` and `CONTEXT.md`, when configured
- nearby source files that implement the concepts under discussion

### File structure

Most Alejo repos have a single context:

```text
/
|-- CONTEXT.md
|-- docs/
|   |-- adr/
|   `-- agents/
`-- src/
```

If a `CONTEXT-MAP.md` exists at the root, the repo has multiple contexts. The map points to where each one lives:

```text
/
|-- CONTEXT-MAP.md
|-- docs/
|   `-- adr/              # system-wide decisions
`-- src/
    |-- ordering/
    |   |-- CONTEXT.md
    |   `-- docs/adr/     # context-specific decisions
    `-- billing/
        |-- CONTEXT.md
        `-- docs/adr/
```

Create files lazily, only when there is something to write. If no `CONTEXT.md` exists, create one when the first project-specific term is resolved. If no `docs/adr/` exists, create it when the first ADR is needed. Always create the final Alejo Questions session log at the end, even if no glossary or ADR changed. In Linear-configured repos, collect local Q&A, `CONTEXT.md`, and ADR changes during the session, then publish or update the Linear Project Documents named `Q&A` and `CONTEXT.md` once at session close without asking for confirmation; local files are working copies or mirrors, not the canonical published artifact.

## During the session

Every Alejo Questions prompt must be multiple choice. Keep options short, mark the recommended option, explain why it is recommended, explain why the other options are interesting or viable, and include an "Other / correction" option when the listed choices may not cover the user's intent.

### Relentless question queue

Before the first question, identify the current question queue from the product clarity checklist, domain-language gaps, code/doc contradictions, and any optional technical track the user has chosen. The queue can evolve as answers reveal new branches.

After each answer, do exactly one of these:

- Ask the next highest-priority unanswered multiple-choice question.
- If the product queue is exhausted, show the product snapshot and ask whether to enter technical decisions.
- If all active queues are exhausted or the user explicitly stops, write the final session log and publish the final Linear updates.

Do not end a turn with an idle prompt such as "let me know when to continue" while unanswered questions remain. Only mark the session complete after every active branch has either been answered, explicitly deferred, or marked unresolved in the Q&A log.

### Goal loop

Keep the product clarity goal visible. After each answer, update a compact goal check:

```md
Goal check: {achieved | still missing}
Clear: {1-3 settled items}
Still missing: {next uncertainty}
```

Choose the next question based on the most important missing product clarity item. Do not drift into technical choices until the product goal is achieved and the user opts into technical decisions. Keep asking product questions until the goal checklist is covered; the user should not need to prompt the session to continue.

When the goal is achieved, summarize the product snapshot before asking about technical decisions:

```md
Product snapshot:
- User:
- Pain/job:
- Value proposition:
- Core experience:
- Success signals:
- Scope boundaries:
- Open risks:
```

### Challenge against the glossary

When the user uses a term that conflicts with the existing language in `CONTEXT.md`, call it out immediately. Example: "Your glossary defines 'cancellation' as X, but you seem to mean Y. Which should we use? A) Existing glossary meaning (recommended, keeps language stable), B) New meaning from this plan (viable if the domain language has changed), C) Other / correction."

### Sharpen fuzzy language

When the user uses vague or overloaded terms, propose a precise canonical term. Example: "You're saying 'account'. Which term should this be? A) Customer (recommended, matches the business actor), B) User (viable if this is about authentication), C) Other / correction."

When one word names multiple concepts, separate the concepts and present the meanings as options. When multiple words name the same concept, pick one canonical term and list the others as terms to avoid.

### Discuss concrete scenarios

When domain relationships are being discussed, stress-test them with concrete scenarios. Invent edge cases that force precision around boundaries, ownership, cardinality, lifecycle, failure modes, and cross-context behavior.

### Cross-reference with code and docs

When the user states how something works, check whether the code agrees. If you find a contradiction, surface it plainly. Example: "The code cancels entire Orders, but the plan assumes partial cancellation is possible. Which source should change? A) Adjust the plan to match whole-order cancellation (recommended, smallest change), B) Change the domain to support partial cancellation (viable if the new behavior is required), C) Other / correction."

When docs contradict code, present the likely resolutions as options: documentation is stale, implementation is wrong, or the plan should be adjusted.

### Update CONTEXT.md locally

When a project-specific term or relationship is resolved, update the relevant `CONTEXT.md` locally right there. Do not batch local glossary edits. Use the format in [context-format.md](./references/context-format.md).

`CONTEXT.md` must stay devoid of implementation details. Do not treat it as a spec, scratch pad, or repository for implementation decisions. It is a glossary and relationship map.

If the repo is configured for Linear Project Documents, do not sync the Project document named `CONTEXT.md` after each question or glossary update. Add the final local `CONTEXT.md` content to the session-close publish batch and sync it once after the whole Q&A is done.

### Offer ADRs sparingly

Only offer to create an ADR when all three are true:

1. Hard to reverse: the cost of changing the decision later is meaningful.
2. Surprising without context: a future reader would wonder why this path was chosen.
3. Real trade-off: there were meaningful alternatives and one was selected for specific reasons.

If any of the three is missing, skip the ADR. When the decision qualifies and is settled, create or update the ADR locally using [adr-format.md](./references/adr-format.md). Keep asking any remaining questions that could change the ADR before treating it as final.

### Keep the Q&A record

For every question, record the issue being tested, options given, recommended answer, rationale for the recommendation, why other options were viable, user answer, evidence checked, resolution, and docs changed. Record only visible questions, recommendations, answers, evidence, and outcomes. Do not include hidden reasoning.

### Write the final session log

At the end of every Alejo Questions session, create a Markdown log using [session-log-format.md](./references/session-log-format.md).

Default path:

```text
docs/questions/YYYY-MM-DD-<topic-slug>.md
```

If the repository has a different Alejo documentation convention, follow it while keeping the file easy to find. If the session stops early, create the log with the Q&A collected so far and mark unresolved items clearly.

Include the original plan or summary, every question asked, every recommended answer, the user's answers or corrections, evidence from code or docs, resolved terminology and relationships, ADRs created or updated, open questions, follow-ups, and unresolved contradictions.

In Linear-configured repos, publish the final log to the Linear Project document named `Q&A` at session close. If the Project already has a `Q&A` document, update it in place with the latest session rather than creating a Linear issue. Publish the final `CONTEXT.md` Project document in the same closing batch, not during each answer.

</supporting-info>
