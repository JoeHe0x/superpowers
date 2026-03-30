# DD Template

Use this template for `docs/dd/<jira-key-or-topic>.md`.

```markdown
# <Title>

## Metadata
- Tracker: `JIRA-123` or `none`
- Sources:
  - Jira:
  - Confluence:
  - Local docs:
- Source snapshot retrieved at:
- Source status / revision:
- Repository area:
- Execution harness: local shell | devcontainer | CI | other
  <!-- Execution harness = where verification commands actually run.
       local shell: developer machine with dependencies installed locally.
       devcontainer: VS Code / GitHub Codespaces container defined in .devcontainer/.
       CI: verification only possible in the pipeline (e.g. missing secrets or infra locally).
       other: describe the environment (e.g. remote SSH host, Kubernetes exec). -->
- Status: Draft | In Review | Approved | Implemented

## Requirement Snapshot
- Key requirement excerpts:
- Acceptance criteria copied or normalized from source:
- Missing or inaccessible sources:

## Problem Statement
What business or user problem is being solved?

## Scope
### In Scope
- 

### Out of Scope
- 

## Current-State Findings
- Relevant modules:
- Existing APIs:
- Existing tests:
- Constraints discovered from code/docs:

## Refined Requirements
### Functional
- 

### Non-Functional
- 

## Assumptions and Risks
- Assumptions:
- Risks:
- Dependencies:

## Acceptance Criteria
- [ ] 
- [ ] 

## Traceability
| Requirement / Criterion | Planned tests | Expected files / modules |
|---|---|---|
|  |  |  |

## Design Approach
- Entry points:
- Core components:
- Data flow:
- Migration or compatibility notes:

## Open Questions
- 

## Review Log
- Reviewer:
- Reviewed at:
- Decision:
- Approval scope:
- Notes:

## Implementation Evidence
- Plan:
- Tests:
- Branch:
- Build command and result:
- Startup command and result:
- Build verification:
- Runtime verification:
- API verification:
- Tracker update link or note:

## Final Summary
- What changed:
- Deviations from original requirement:
- Follow-up work:
- Jira/Confluence update summary:
```