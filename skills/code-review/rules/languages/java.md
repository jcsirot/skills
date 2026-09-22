# Java and JVM Review Guide

Apply this guide to Java code, JVM build files, and visible Spring, Quarkus, or
Jakarta EE integrations. Confirm the Java and framework versions before
treating a language feature or framework behavior as available.

## Code quality, correctness, and performance

- Check nullability contracts, defensive boundaries, and whether
  `Optional`/annotations are used consistently rather than as a blanket
  replacement for domain modeling.
- Check exception taxonomy and propagation. Broad catches, swallowed causes,
  checked exceptions converted to empty results, and retries without
  idempotency often hide correctness failures.
- Check `equals`/`hashCode`, mutability, collection choice, generics, boxing,
  and thread-safety when values cross caches, sets, maps, or concurrent code.
- Check resource ownership: use try-with-resources for streams, files,
  sockets, JDBC resources, and other `AutoCloseable` values.
- For Spring/JPA/Hibernate, inspect transaction boundaries, lazy loading,
  N+1 queries, entity mutation, pagination, fetch plans, and connection-pool
  behavior. Do not recommend eager loading without checking the query shape.
- For Quarkus, inspect CDI scopes and proxies, build-time augmentation,
  extension configuration, RESTEasy Reactive boundaries, transactional
  behavior, blocking work on event-loop threads, and native-image
  compatibility. Check that reflection, serialization, resource, and proxy
  registrations required by native builds are explicit and tested.
- Check executor, `CompletableFuture`, virtual-thread, and reactive pipelines
  for unbounded queues, blocking work on the wrong scheduler, missing
  cancellation, and shutdown/ownership paths.
- Check tests for boundary values, transaction rollback, concurrency, and
  framework wiring rather than only happy-path service calls.

## Security

- For JDBC, JPA, and query builders, verify parameterization and inspect
  dynamically constructed fragments such as sort columns or table names.
- For Spring Security and Jakarta Security, verify authentication,
  method-level and object-level authorization, tenant isolation, CSRF
  behavior, session/cookie settings, and mass-assignment boundaries.
- For Quarkus Security, verify HTTP and annotation-based authorization,
  identity propagation, role checks on REST and reactive endpoints, security
  events, and configuration profiles. Ensure development/test security
  settings cannot leak into production.
- Treat Java native serialization, unsafe Jackson polymorphic typing, XML
  external entities, expression languages, and template engines as
  high-risk deserialization or injection boundaries.
- Check URL fetching, redirects, file uploads, archive extraction, and
  `ProcessBuilder` calls for SSRF, traversal, command injection, and resource
  exhaustion.
- Verify secrets are absent from source, configuration committed to the
  repository, logs, actuator/management endpoints, and exception messages.
- Check password hashing, token verification, TLS/certificate validation, and
  cryptographic randomness against the project's supported libraries.
- Check dependency and plugin changes in Maven/Gradle for unsafe versions,
  permissive defaults, repository changes, and exposed debug functionality.
- For Quarkus extensions and native builds, inspect extension versions,
  build-time configuration, enabled management/health endpoints, dev services,
  native substitutions, and any secrets or credentials exposed through
  application or management configuration.
