# Traceability Examples

Use these patterns to map requirements to tests and changed files in the DD.

## Rules

- Map each acceptance criterion to at least one planned test
- Prefer requirement language over implementation language
- List expected files or modules, not speculative refactors
- If one test covers multiple criteria, say so explicitly

## Example 1: New API Validation Rule

```markdown
## Acceptance Criteria
- [ ] Reject requests whose `name` is blank with HTTP 400 and error code `INVALID_NAME`
- [ ] Preserve existing success response for valid requests

## Traceability
| Requirement / Criterion | Planned tests | Expected files / modules |
|---|---|---|
| Reject blank `name` with HTTP 400 and `INVALID_NAME` | Controller test for blank `name`; service validation unit test | `UserController`, `UserService`, request DTO validator |
| Preserve success response for valid requests | Existing happy-path controller test updated only if contract changes | `UserController`, existing API test fixture |
```

## Example 2: Scheduled Job Behavior Change

```markdown
## Acceptance Criteria
- [ ] Process only active accounts
- [ ] Emit one warning log per skipped inactive account

## Traceability
| Requirement / Criterion | Planned tests | Expected files / modules |
|---|---|---|
| Process only active accounts | Job unit test with mixed active and inactive fixtures | scheduler job class, account query helper |
| Emit warning log for skipped inactive account | Logging-focused unit test or integration test with captured logger output | scheduler job class |
```

## Example 3: Bug Fix With Regression Test

```markdown
## Acceptance Criteria
- [ ] Duplicate submissions with the same idempotency key return the original result
- [ ] No second downstream call is made

## Traceability
| Requirement / Criterion | Planned tests | Expected files / modules |
|---|---|---|
| Duplicate submission returns original result | Regression test that submits the same key twice | handler/service, idempotency store test |
| No second downstream call is made | Unit test asserting downstream dependency invoked once | service unit test, dependency stub |
```

## Anti-Patterns

- "Add tests" with no criterion mapping
- Mapping tests to internal helper methods instead of user-visible behavior
- Listing the whole subsystem as expected files
- Treating manual checks as the only verification for a functional requirement
