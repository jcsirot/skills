# Quarkus Review Guide

Apply this guide only when `pom.xml` contains a Quarkus marker listed in
`rules/tech-domains/index.md`. Confirm the Quarkus platform and extension versions
before relying on build-time behavior, defaults, or native-image support.

## Code quality, correctness, and performance

- Inspect CDI scopes and proxies, build-time augmentation, extension
  configuration, and RESTEasy Reactive endpoint behavior. Verify that
  configuration and beans available in development are also correctly
  available in production.
- Check transaction boundaries and reactive behavior. Identify blocking work
  on event-loop threads and verify that reactive endpoints use compatible
  APIs.
- Check executors, scheduled work, and asynchronous pipelines for unbounded
  queues, missing cancellation, and lifecycle or shutdown gaps.
- For native builds, verify required reflection, serialization, resource, and
  proxy registrations, and test the affected behavior in the native profile
  when the repository supports it.
- Verify tests cover relevant CDI, REST, transaction, configuration, and
  native-build behavior rather than only isolated service logic.

## Security

- For Quarkus Security, verify HTTP and annotation-based authorization,
  identity propagation, role checks on REST and reactive endpoints, and
  object-level or tenant permissions. Check security-event handling where
  relevant.
- Check security configuration and profiles so development/test settings,
  dev services, and permissive defaults cannot leak into production.
- Inspect enabled management and health endpoints, build-time configuration,
  native substitutions, and secrets or credentials exposed through
  application or management configuration.
- Check Quarkus extension and plugin versions, dependency sources, and build
  configuration for insecure defaults or unexpected build-time behavior.
- Review serialization and deserialization, URL fetching, file handling, and
  process execution at the relevant trust boundaries using the shared
  security checklist.
