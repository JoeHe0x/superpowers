# DD Template

Use this template for `docs/dd/<jira-key-or-topic>.md`.

This is the full, general-purpose DD template.
- Keep the sections that add signal.
- Delete sections that are irrelevant.
- Mark unknowns explicitly instead of inventing details.
- Use short bullets unless deeper explanation is necessary.

```markdown
# <Title>

## Metadata
- Tracker: `JIRA-123` or `none`
- Topic / slug:
- Sources:
  - Jira:
  - Confluence:
  - Local docs:
  - Chat / meeting notes:
- Source snapshot retrieved at:
- Source status / revision:
- Repository area:
- Execution harness: local shell | devcontainer | CI | other
  <!-- Execution harness = where verification commands actually run.
       local shell: developer machine with dependencies installed locally.
       devcontainer: VS Code / GitHub Codespaces container defined in .devcontainer/.
       CI: verification only possible in the pipeline (e.g. missing secrets or infra locally).
       other: describe the environment (e.g. remote SSH host, Kubernetes exec). -->
- Status: Draft | In Review | Confirmed | Implemented

## Requirement Snapshot
- Business goal:
- User or stakeholder:
- Key requirement excerpts:
- Acceptance criteria or verification notes copied or normalized from source:
- Missing or inaccessible sources:

## Problem Statement
- Problem to solve:
- Why now:
- Desired outcome:
- Non-goals:

## Scope
### In Scope
- 

### Out of Scope
- 

## Stakeholders And Interfaces
- Requester / owner:
- Affected users:
- Upstream systems:
- Downstream systems:
- External interfaces:

## Current-State Findings
- Relevant modules:
- Existing APIs:
- Existing UI / UX behavior:
- Existing data model or schema:
- Existing tests:
- Constraints discovered from code/docs:

## Existing Behavior Summary
- Current behavior:
- Known pain points:
- Current workaround, if any:

## Refined Requirements
### Functional
- 

### Non-Functional
- 

### Operational / Delivery
- Logging / observability:
- Performance / scale:
- Security / permissions:
- Migration / rollout:
- Backward compatibility:

## Assumptions and Risks
- Assumptions:
- Risks:
- Dependencies:

## Options Considered
### Option A
- Summary:
- Pros:
- Cons:

### Option B
- Summary:
- Pros:
- Cons:

### Chosen Direction
- Decision:
- Why this option:
- Why not the others:

## Acceptance Criteria / Verification Notes
- [ ] 
- [ ] 

## Traceability
| Requirement / Behavior | Planned tests or checks | Expected files / modules |
|---|---|---|
|  |  |  |

## Design Approach
- Entry points:
- Core components:
- Data flow:
- API / contract changes:
- Data model changes:
- State management or lifecycle notes:
- Error handling:
- Observability:
- Migration or compatibility notes:

## Implementation Plan Outline
- Step 1:
- Step 2:
- Step 3:

## Verification Strategy
- Unit tests:
- Integration tests:
- Manual checks:
- API / contract checks:
- Rollback or fallback checks:

## Open Questions
- 

## Review Log
- Confirmed by:
- Confirmed at:
- Decision:
- Confirmation scope:
- Deferred items:
- Notes:

## Implementation Evidence
- Plan:
- Tests:
- Branch:
- Commits / PR:
- Build command and result:
- Startup command and result:
- Build verification:
- Runtime verification:
- API verification:
- UI verification:
- Data verification:
- Observability verification:
- Tracker update link or note:

## Final Summary
- What changed:
- Deviations from original requirement:
- Deferred follow-up:
- Follow-up work:
- Jira/Confluence update summary:
```
