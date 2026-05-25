# Alejo Questions Session Log Format

Create one Markdown file at the end of each Alejo Questions session.

Default path:

```text
docs/questions/YYYY-MM-DD-<topic-slug>.md
```

## Template

```md
# Alejo Questions: {Topic}

- **Date**: {YYYY-MM-DD}
- **Repository**: {repo name or path}
- **Plan under review**: {short summary or link/path}
- **Context docs touched**: {files or "None"}
- **ADRs created or updated**: {files or "None"}
- **Goal**: Clear product experience and end-user value proposition
- **Goal status**: {achieved | stopped early | blocked}
- **Technical decisions covered**: {yes | no}
- **Status**: {complete | stopped early | blocked}
- **Question coverage**: {all active branches answered | deferred branches named | stopped before queue was exhausted}

## Session Summary

{Brief summary of what changed in the shared understanding.}

## Product Snapshot

- **Target user**: {who the experience is for}
- **Pain/job**: {what problem, desire, or job is being addressed}
- **Value proposition**: {the promised outcome for the end user}
- **Core experience**: {short description of the main journey}
- **Success signals**: {observable signs the experience works}
- **Scope boundaries**: {main in/out of scope boundaries}
- **Open risks**: {remaining product risks or "None"}

## Questions And Answers

### 1. {Question}

- **Recommended answer**: {recommendation given before asking}
- **User answer**: {user's answer, correction, or confirmation}
- **Evidence checked**: {code/docs inspected, or "None"}
- **Resolution**: {settled answer, contradiction, or open point}
- **Docs updated**: {files changed, or "None"}

### 2. {Question}

- **Recommended answer**: {recommendation}
- **User answer**: {answer}
- **Evidence checked**: {evidence}
- **Resolution**: {resolution}
- **Docs updated**: {files}

## Resolved Language

- **{Term}**: {definition or relationship resolved during the session}

## Decisions

- {Decision made, with ADR link if one was created}

## Technical Decisions

- {Technical decision, trade-off, or "Not covered"}

## Open Questions

- {Question that remains unresolved, owner if known, and next step}

## Follow-Ups

- {Documentation, code, test, or planning action to take next}
```

## Rules

- Record every visible question asked during the session.
- Preserve the recommendation that accompanied each question.
- Capture the user's actual answer or correction.
- Include the goal status and final product snapshot.
- Mark whether the user chose to cover technical decisions.
- Mark `Status: complete` only after every active question branch was answered, explicitly deferred, or marked unresolved.
- If stopped early, name the next unanswered branch so the session can resume without the user needing to reconstruct it.
- Link to files when evidence came from code or docs.
- Mark unresolved contradictions directly instead of smoothing them over.
- Do not include hidden reasoning or private deliberation.
