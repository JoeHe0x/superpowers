# DD To Plan And Test Handoff

Use this after DD approval and before implementation starts.

## Entry Criteria

Do not move to plan writing until the DD includes:
- Requirement sources and snapshot metadata
- In-scope and out-of-scope behavior
- Acceptance criteria clear enough to test
- Open questions either resolved or explicitly deferred
- A traceability table with at least initial planned tests
- Review approval recorded

## Handoff Contract To `writing-plans`

When invoking the planning skill, pass these expectations:
- The DD is the authority
- Plan tasks must preserve requirement-to-test traceability
- File paths must be concrete
- Commands must be runnable
- The first implementation step for each behavior should be a failing test or test scaffold

## Deriving Tests From Acceptance Criteria

For each criterion, decide:
- Unit test, integration test, API test, or a combination
- Narrowest failing test that proves the behavior is missing
- Preconditions, fixtures, and dependencies
- Observable outcome: response, state change, event, log, or side effect

Use this checklist:

```markdown
| Criterion | Test type | First failing test | Observable outcome |
|---|---|---|---|
|  |  |  |  |
```

## Review Gate Before Coding

The human should be able to answer yes to both:
- Does the plan implement exactly the approved DD?
- Do the planned tests cover every acceptance criterion?

If either answer is no:
- Update the DD first if requirements changed
- Otherwise revise the plan and tests

## Scope Control

If implementation discovers new behavior:
- Stop
- Update the DD
- Reconfirm approval before expanding the plan

Do not let the plan become the new source of truth. The DD remains authoritative.
