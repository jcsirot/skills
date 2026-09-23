# Code Quality Checklist

Evaluate maintainability and robustness using the principles that apply to the
reviewed change:

Use `rules/languages/index.md` to select language and framework-specific
quality guidance. Do not transfer idioms from one language to another; for
mixed-language changes, apply each relevant guide independently.

1. **Correctness and edge cases**
   - Are `null`/`undefined`, empty collections, boundaries, invalid states,
     retries, timeouts, partial failures, and cancellation handled correctly?
   - Are operations idempotent where retries or duplicate messages are possible?
   - Are concurrency, ordering, and race conditions addressed where relevant?

2. **Error handling and compatibility**
   - Is error handling explicit, observable, and free of silent catches or
     success-shaped fallbacks?
   - Do API, schema, migration, serialization, and configuration changes
     preserve compatibility or provide a safe rollout path?

3. **Readability and design**
   - Are responsibilities, names, control flow, and abstractions clear?
   - Is the code DRY without over-engineering, and is complexity justified by
     the behavior being implemented?
   - Does the change follow established project patterns instead of adding a
     duplicate helper or inconsistent convention?

4. **Performance and resource lifecycle**
   - Are there N+1 queries, unindexed or unbounded queries, repeated expensive
     work, unnecessary allocations, or blocking operations?
   - Are listeners, streams, files, transactions, connections, and timers
     closed on every relevant path?

5. **Testing and operability**
   - Do tests cover the changed behavior, affected existing behavior, failure
     paths, and important boundaries without relying on brittle timing or
     implementation details?
   - Does the test suite cover all changed contracts and their existing
     callers, consumers, adapters, migrations, and configuration paths?
   - When coverage is insufficient, propose focused unit tests with concrete
     scenarios and assertions. Prefer unit tests for local logic and add
     integration or contract tests when the risk crosses a process boundary.
   - Are logs, metrics, traces, feature flags, and rollback behavior sufficient
     for the risk and production impact of the change?