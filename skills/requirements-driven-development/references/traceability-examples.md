# Traceability Examples

Use these patterns to fill the unified DD template in a way that keeps requirements, design, and verification aligned.

These are partial examples, not full DDs.
- Copy only the sections that add signal.
- Keep the wording close to the requirement source when possible.
- Show traceability through the DD, not just through a single table.

## Rules

- Map the behaviors that matter to at least one planned test or verification check
- Prefer requirement language over implementation language
- List expected files or modules, not speculative refactors
- If one test covers multiple criteria, say so explicitly
- For tiny low-risk changes, a full matrix is optional if the verification approach is already obvious

## Example 1: New API Validation Rule

```markdown
## Requirement Snapshot
- Business goal: Prevent invalid names from entering the system.
- Key requirement excerpts:
  - Requests with blank `name` must be rejected.
  - Existing valid request behavior must remain unchanged.

## Acceptance Criteria / Verification Notes
- [ ] Reject requests whose `name` is blank with HTTP 400 and error code `INVALID_NAME`
- [ ] Preserve existing success response for valid requests

## Design Approach
- Entry points: `UserController#create`, request DTO validation
- Core components: controller validation path, service guard
- API / contract changes: none for successful requests; explicit error response for invalid input

## Traceability
| Requirement / Behavior | Planned tests | Expected files / modules |
|---|---|---|
| Reject blank `name` with HTTP 400 and `INVALID_NAME` | Controller test for blank `name`; service validation unit test | `UserController`, `UserService`, request DTO validator |
| Preserve success response for valid requests | Existing happy-path controller test updated only if contract changes | `UserController`, existing API test fixture |

## Verification Strategy
- Unit tests: service validation rejects blank `name`
- Integration tests: controller returns HTTP 400 and `INVALID_NAME`
- API / contract checks: happy path response remains backward compatible
```

## Example 2: Scheduled Job Behavior Change

```markdown
## Problem Statement
- Problem to solve: The job currently processes inactive accounts and creates noisy downstream work.
- Desired outcome: Only active accounts are processed, and skipped inactive accounts are visible in logs.

## Refined Requirements
### Functional
- Process only active accounts.
- Emit one warning log per skipped inactive account.

## Acceptance Criteria / Verification Notes
- [ ] Process only active accounts
- [ ] Emit one warning log per skipped inactive account

## Design Approach
- Entry points: scheduled job runner
- Core components: account query filter, job execution loop
- Observability: warning log for each skipped inactive account

## Traceability
| Requirement / Behavior | Planned tests | Expected files / modules |
|---|---|---|
| Process only active accounts | Job unit test with mixed active and inactive fixtures | scheduler job class, account query helper |
| Emit warning log for skipped inactive account | Logging-focused unit test or integration test with captured logger output | scheduler job class |

## Verification Strategy
- Unit tests: mixed fixture test proves inactive accounts are skipped
- Manual checks: review local log output during a controlled run if needed
- Observability verification: warning log format and count match skipped accounts
```

## Example 3: Bug Fix With Regression Test

```markdown
## Existing Behavior Summary
- Current behavior: duplicate submissions with the same idempotency key may trigger duplicate downstream calls.
- Known pain points: users can receive inconsistent outcomes and downstream systems perform duplicate work.

## Refined Requirements
### Functional
- Duplicate submissions with the same idempotency key must return the original result.
- No second downstream call should be made for the same key.

## Acceptance Criteria / Verification Notes
- [ ] Duplicate submissions with the same idempotency key return the original result
- [ ] No second downstream call is made

## Design Approach
- Core components: request handler, idempotency store, downstream client wrapper
- Error handling: replay stored result when duplicate key is detected

## Traceability
| Requirement / Behavior | Planned tests | Expected files / modules |
|---|---|---|
| Duplicate submission returns original result | Regression test that submits the same key twice | handler/service, idempotency store test |
| No second downstream call is made | Unit test asserting downstream dependency invoked once | service unit test, dependency stub |

## Implementation Evidence
- Tests: regression test for duplicate key; downstream invocation count assertion
- Runtime verification: optional local replay with captured dependency stub output
```

## Example 4: Frontend Form Validation

```markdown
## Stakeholders And Interfaces
- Affected users: end users submitting the form
- External interfaces: browser form interaction only

## Refined Requirements
### Functional
- Submit button stays disabled until all required fields are non-empty.
- Inline error message appears beneath each invalid field on blur.

## Acceptance Criteria / Verification Notes
- [ ] Submit button is disabled until all required fields are non-empty
- [ ] Inline error message appears beneath each invalid field on blur

## Design Approach
- Entry points: form container, field blur handlers
- State management or lifecycle notes: field touched state drives error rendering

## Traceability
| Requirement / Behavior | Planned tests | Expected files / modules |
|---|---|---|
| Submit disabled until required fields filled | Component test asserting button `disabled` state with empty vs. filled fixture | `SubmitButton`, `FormContainer` |
| Inline error on blur | Component test simulating blur on empty field, asserting error message rendered | field components, validation hook/util |

## Verification Strategy
- Unit tests: validation hook or utility behavior
- Integration tests: component interaction with blur and button state
- Manual checks: quick browser confirmation of focus/blur behavior
```

## Example 5: Configuration or Feature-Flag Change

```markdown
## Scope
### In Scope
- Enable Feature X only when `FEATURE_X_ENABLED=true`
- Preserve existing default behavior when the flag is absent or false

### Out of Scope
- Any redesign of Feature X behavior itself

## Acceptance Criteria / Verification Notes
- [ ] Feature X is active only when `FEATURE_X_ENABLED=true`
- [ ] Default behavior is preserved when the flag is absent or false

## Design Approach
- Entry points: configuration loader, feature guard
- Migration or compatibility notes: default behavior remains unchanged for existing deployments

## Traceability
| Requirement / Behavior | Planned tests | Expected files / modules |
|---|---|---|
| Feature X active when flag is true | Unit test with env var set to `true` | config loader, feature guard |
| Default behavior preserved when flag absent | Unit test with env var unset; existing behavior assertions unchanged | config loader, affected service |

## Verification Strategy
- Unit tests: env var true / false / unset cases
- Manual checks: local startup with and without the flag if configuration loading is environment-sensitive
```

## Anti-Patterns

- Writing only "add tests" with no link back to the DD sections
- Mapping tests to internal helper methods instead of user-visible behavior
- Listing the whole subsystem as expected files instead of the likely change surface
- Treating manual checks as the only verification for a functional requirement
- Filling every DD section even when it adds no signal
