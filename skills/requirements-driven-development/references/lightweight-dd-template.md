# Lightweight DD Template

Use this when the skill is in lightweight RDD mode: localized change, explicit requirements, low risk, and no cross-service or schema design.

Keep traceability. Reduce prose.

```markdown
# <Title>

## Metadata
- Tracker: `JIRA-123` or `none`
- Sources:
  - Primary:
  - Supporting:
- Source snapshot retrieved at:
- Source status / revision:
- Repository area:
- Execution harness:
- Status: Draft | In Review | Approved | Implemented

## Requirement Snapshot
- Business goal:
- In scope:
- Out of scope:
- Acceptance criteria:
- Missing or inaccessible sources:

## Current-State Findings
- Relevant files or modules:
- Existing behavior:
- Constraints:

## Decisions
- Chosen approach:
- Assumptions:
- Dependencies:
- Risks:

## Open Questions
- 

## Traceability
| Criterion | Planned test | Expected files |
|---|---|---|
|  |  |  |

## Review Log
- Reviewer:
- Reviewed at:
- Decision:
- Notes:

## Implementation Evidence
- Plan:
- Tests:
- Branch:
- Verification commands and results:

## Final Summary
- What changed:
- Deviations:
- Follow-up work:
```

## Minimum Bar

Do not use the lightweight template unless all of these are true:
- Requirements are already explicit
- The change is localized
- No public API, schema, or cross-service design is involved
- Open questions are minor enough to defer explicitly

Escalate to the full DD template if scope expands during analysis.
