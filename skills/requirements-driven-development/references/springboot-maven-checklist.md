# Spring Boot Maven Checklist

Use this checklist when the target project is a Java Spring Boot Maven service.

## Discover
- Find the owning `pom.xml`
- Identify the module that contains the changed controller, service, repository, and tests
- Check whether the project already uses `MockMvc`, `WebTestClient`, Testcontainers, or slice tests
- Record the execution harness you will use: local shell, devcontainer, CI, or another approved runtime

## Before Coding
- Capture the current build and test command in the DD
- Identify the narrowest test target that should fail first
- Place unit tests under `src/test/java/...` following existing package structure
- Note any required profiles, env vars, containers, or secrets needed to start the service

## During Implementation
- Prefer JUnit 5 and the project's current mocking style
- For HTTP endpoints, follow existing API test style before introducing a new one
- Keep configuration changes explicit in `application-*.*`, `bootstrap.*`, or test fixtures

## Verification
- Run focused tests first
- Run the relevant Maven compile or package command
- Start the service locally with the repo's normal command
- Check `application-*.*` and `bootstrap.*` for port, `server.servlet.context-path`, and actuator settings, then confirm the effective values from startup logs
- Hit the changed API path with a real request and capture the result
- Record exact commands, profiles, and outcomes in the DD

## Suggested Commands
```bash
mvn test
mvn -DskipTests compile
mvn spring-boot:run
# Replace the port, context path, and endpoint with the values confirmed from config and startup logs.
curl -i "http://localhost:8080<server.servlet.context-path>/actuator/info"
```

Replace commands with module-specific or repo-specific variants when needed.
