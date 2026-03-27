# Spring Boot Documentation Analysis Checklist

Use this checklist before finalizing the generated document.

## Endpoint Discovery

- Confirm all controller entry points: `@RestController`, `@Controller`, and composite annotations.
- Combine class-level and method-level mappings into the final path.
- Capture HTTP method, media types, version prefix, and deprecated endpoints if present.
- Check generated OpenAPI metadata, `@Operation`, `@ApiOperation`, or Swagger config as hints, not the final source of truth.

## Request and Response Shape

- Identify request DTOs, path variables, query params, headers, and multipart inputs.
- Check validation annotations such as `@Valid`, `@Validated`, `@NotNull`, `@NotBlank`, size limits, enum restrictions, and custom validators.
- Note serialization rules that change payloads, including Jackson annotations, custom serializers, or hidden fields.
- Record the actual response type, wrappers, pagination shape, and error envelope.

## Business Flow Tracing

- Resolve controller method to service method.
- Trace branch conditions, permission checks, feature flags, and fallback logic.
- Identify transaction boundaries such as `@Transactional` or explicit transaction helpers.
- Record persistence changes, repository queries, optimistic locking, and soft-delete behavior.
- Record outbound calls to MQ, cache, HTTP clients, RPC clients, file storage, or schedulers.
- Check for async side effects such as events, listeners, or `@Async` flows.

## Cross-Cutting Concerns

- Inspect Spring Security config, `@PreAuthorize`, filters, and interceptors.
- Inspect `@ControllerAdvice`, exception translators, and global response wrappers.
- Inspect `@Profile`, `@ConditionalOnProperty`, and config values that materially change behavior.
- Inspect idempotency, retry, rate limit, or deduplication logic when present.

## Evidence Quality

- Prefer `jdtls-lsp` for definition, references, implementations, and call hierarchy when available.
- Fallback to targeted search only after language-server navigation is unavailable or insufficient.
- Use tests to confirm behavior, fixtures, and error cases.
- Use git or GitNexus only to explain intent or history, not to override current code behavior.
- Mark inferences explicitly when code leaves room for ambiguity.

## Output Quality Gate

- Every endpoint in the inventory has a matching detail section.
- Every detail section includes route, request, response, business flow, side effects, and evidence.
- Cross-cutting behavior is documented once and referenced consistently.
- The final document states whether verification was static only or included runtime execution.