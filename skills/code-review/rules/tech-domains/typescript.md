# TypeScript Review Guide

Apply this guide to TypeScript source and TypeScript build or configuration
changes. Load `nodejs.md` and/or `browser.md` for runtime-specific concerns
using the signals in `rules/tech-domains/index.md`. Distinguish compile-time types
from runtime validation because TypeScript types are erased at runtime.

## Code quality, correctness, and performance

- Check strictness settings, `any`, unsafe assertions, non-null assertions,
  index access, widening, discriminated unions, and generic constraints at
  trust boundaries.
- Verify external input with runtime schemas or explicit guards before using
  it as a typed value. Check that validation and transformation preserve the
  intended domain invariants.
- Check promise rejection handling, cancellation, and unhandled errors.
- Check module boundaries, import cycles, generated types, declaration output,
  and compatibility of public APIs. Load the runtime guide for module-system
  or bundler-specific behavior.
- Check unnecessary object/array copies, repeated serialization, and
  unbounded caches.
- Check tests for runtime-invalid inputs, serialization, time zones, numeric
  boundaries, and failure paths.

## Security

- Check prototype pollution, unsafe object merging, dynamic evaluation
  (`eval`, `Function`), and SQL/NoSQL query construction where applicable.
- Inspect JSON/URL/form parsing, schema validation, file uploads, and
  deserialization for resource exhaustion and type confusion.
- Check secrets in source, configuration, logs, and error payloads.
- Review npm/pnpm/yarn dependency and lockfile changes for vulnerable
  dependencies or supply-chain risks. Use the relevant runtime guide for
  environment-specific exposure.
