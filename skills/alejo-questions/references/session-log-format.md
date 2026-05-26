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
- **Status**: {complete | stopped early | blocked}

## Session Summary

{Brief summary of what changed in the shared understanding.}

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

## Open Questions

- {Question that remains unresolved, owner if known, and next step}

## Follow-Ups

- {Documentation, code, test, or planning action to take next}
```

## Rules

- Record every visible question asked during the session with its sequential question number.
- Preserve the same question number used in the live Alejo Questions prompt.
- Preserve the recommendation that accompanied each question.
- Capture the user's actual answer or correction.
- Link to files when evidence came from code or docs.
- Mark unresolved contradictions directly instead of smoothing them over.
- Do not include hidden reasoning or private deliberation.
