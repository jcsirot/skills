# Spring Boot Review Guide

Apply this guide only when `pom.xml` contains a Spring Boot marker listed in
`rules/tech-domains/index.md`. Confirm the Spring Boot and Spring Security versions
before relying on version-specific defaults or behavior.

## Code quality, correctness, and performance

- Check starter and auto-configuration interactions, conditional beans,
  configuration properties, and bean override behavior. Verify that the
  configuration active in production is the one the change expects.
- Check bean scopes, dependency injection, and proxy-based behavior. For
  `@Transactional` and similar advice, verify transaction boundaries,
  propagation, rollback behavior, and whether calls actually pass through the
  proxy; account for self-invocation and asynchronous execution.
- For Spring MVC, verify request binding and validation at the boundary,
  exception mapping, and response serialization. For WebFlux, check for
  blocking work on event-loop threads, cancellation, backpressure, and
  non-blocking data access.
- When Spring Data JPA/Hibernate is visible, inspect query shape, transaction
  boundaries, lazy loading, N+1 queries, pagination, fetch plans, and entity
  mutation. Do not recommend eager loading without evidence from the query and
  call path.
- Check externalized configuration, profile-specific behavior, startup and
  shutdown lifecycle, and whether actuator or management endpoints are
  intentionally exposed.
- Verify tests cover relevant Spring wiring and configuration, not only
  isolated service methods.

## Security

- For Spring Security, inspect filter-chain ordering and request matchers,
  default-deny behavior, method-security activation, and authorization of the
  specific object and tenant. Do not assume an annotation is enforced without
  verifying the required configuration.
- Check authentication, session fixation protections, cookie flags, CSRF
  behavior, and OAuth2/OIDC or JWT validation against the application's
  authentication model.
- Check request binding and deserialization for mass assignment, unsafe
  polymorphic typing, and validation gaps at controller boundaries.
- Verify actuator and management endpoints, debug settings, and development
  profiles do not expose sensitive operations or configuration in production.
- Check secrets in Spring configuration, environment/profile files, logs,
  actuator responses, and exception messages.
