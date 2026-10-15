# Kotlin Review Guide

Apply this guide to Kotlin/JVM, Android, Kotlin Multiplatform, Gradle Kotlin
DSL, and coroutine-based code. Confirm the Kotlin, JVM, Android, and framework
versions before assuming a language or library feature is available.

## Code quality, correctness, and performance

- Check nullable types, platform types, safe calls, non-null assertions, and
  boundary conversion from Java or external data. Treat `!!` as a finding only
  when the invariant is not established or failure is user-reachable.
- Check sealed hierarchies, exhaustive `when`, data/value classes, equality,
  mutable collections, variance, and extension functions for domain and API
  correctness.
- For coroutines and Flow, check structured concurrency, scope ownership,
  cancellation propagation, dispatcher choice, blocking work, exception
  supervision, hot-flow lifecycle, and collection backpressure.
- Check `suspend` APIs for hidden blocking calls, duplicate work after retries,
  leaked jobs, and lifecycle mismatches in Android or server components.
- Check Java interop, reflection, serialization, default arguments, and
  binary/source compatibility at public boundaries.
- Check resource cleanup with `use`, transaction ownership, thread safety, and
  allocations caused by unnecessary copying or eager collection operations.
- For Android, inspect lifecycle-aware collection, configuration changes,
  main-thread work, saved state, permissions, exported components, and tests
  across relevant lifecycle states.

## Security

- Validate and authorize untrusted data after Kotlin serialization, Jackson,
  reflection, Java serialization, Android intents, deep links, and IPC.
- Check SQL/ORM query parameterization, dynamic query fragments, path handling,
  URL fetching, WebView bridges, and intent redirection for injection,
  traversal, SSRF, and confused-deputy risks.
- For Android, verify exported activities/services/receivers/providers,
  permission checks, pending intents, deep-link validation, and sensitive data
  in logs, preferences, backups, and screenshots.
- Check coroutine exception paths and cancellation so security checks cannot be
  bypassed by a fallback, timeout, supervisor, or swallowed exception.
- Verify secrets are not embedded in APK/client code, Gradle files, source,
  logs, stack traces, or generated configuration.
- Inspect Gradle plugins, dependency resolution, repository configuration, and
  serialization defaults for supply-chain or insecure-default risks.
