---
name: api-docs-gen
description: Use when a Java Spring Boot codebase needs reverse-engineered API documentation and business logic documentation from controllers, DTOs, services, repositories, and integrations, especially for legacy-service onboarding, handoff, audit prep, or undocumented endpoints.
---

# API Docs Gen

## Overview

Use this skill to derive an evidence-backed business logic document from an existing Spring Boot codebase. Treat current code as the primary source of truth, then use tests, OpenAPI annotations, git history, or GitNexus only to clarify intent and fill gaps.

**Announce at start:** "I'm using api-docs-gen to reverse engineer Spring Boot APIs and produce business logic plus API documentation."

## Outputs

Default to one Markdown document unless the service is large.

- Primary doc: `docs/api/<service-or-module>.md`
- Split mode for large services: `docs/api/<service>/index.md` plus one file per controller or domain area

If the repository already has a docs convention or the user gives a target path, follow that instead.

## Fit Check

Use this skill when:

- controllers or endpoints exist but docs are missing, stale, or unreliable
- a legacy Spring Boot service must be onboarded, handed off, or audited
- the user asks for API docs, business logic docs, endpoint docs, workflow docs, or reverse engineering from code
- Swagger or OpenAPI annotations exist but the real controller to service flow still needs explanation

Do not use this skill for greenfield API design. Use it to document current behavior.

## Workflow

1. Scope the surface area. Identify the target module, runtime profile, and package roots. If the request is broad and the service is large, confirm the module or bounded context before documenting everything.
2. Build the API inventory. Find `@RestController`, `@Controller`, `@RequestMapping`, `@GetMapping`, `@PostMapping`, `@PutMapping`, `@PatchMapping`, and `@DeleteMapping`. Resolve class-level and method-level routes, HTTP verbs, auth annotations, validation, request DTOs, response DTOs, and exception mappings.
3. Trace the business flow. Prefer `jdtls-lsp` when available for definition lookup, call hierarchy, references, implementations, and type resolution. Fallback to targeted code search if language-server support is unavailable. Trace each endpoint from controller to service to domain rules to repository, external client, event publisher, cache, or transaction boundary.
4. Corroborate with supporting evidence. Read tests, OpenAPI annotations or generated specs, security config, `@ControllerAdvice`, filters, interceptors, and feature-flag or profile-based config that affects behavior. Use git or GitNexus only to explain why logic exists, never as the primary source of truth over current code.
5. Write the document using `./references/doc-template.md`. If behavior is uncertain, say so explicitly instead of inventing business rules.
6. Review coverage with `./references/springboot-analysis-checklist.md` before finalizing. Every documented endpoint must include both API details and business-flow detail.

## Documentation Rules

- Mirror the user's language. If the user asks in Chinese, write the document in Chinese.
- Separate observed behavior from inferred intent. Label inferences clearly.
- Include evidence for every important claim: class name, method name, and file path.
- Capture cross-cutting concerns once, then reference them from endpoint sections: auth, validation, transactions, exception handling, idempotency, async processing, events, and caching.
- Prefer concise tables for API inventory and short ordered lists for business flow.
- If the service has more than 20 endpoints or more than 5 controllers, split the output by controller or domain.
- If runtime verification is possible, include sample `curl` or `httpie` usage or reference existing integration tests. If not, state that verification was static only.

## Required Coverage

Every endpoint section must answer:

- What route is exposed?
- What request fields and validation rules matter?
- What service method handles it?
- What business rules, branches, and state changes occur?
- What persistence, MQ, cache, or third-party calls happen?
- What success and failure responses are possible?
- What configuration, feature flags, or security constraints affect it?

## Red Flags

Stop and correct course if:

- route paths are copied without combining class-level and method-level mappings
- DTO fields are documented without checking validation or serialization annotations
- service behavior is described without tracing downstream calls
- git history is treated as truth over current code
- undocumented assumptions are presented as facts
- auth, transaction boundaries, or side effects are omitted from the final doc

## Integration

- For Java navigation: `jdtls-lsp`
- For final verification before handing docs back: `verification-before-completion`