# TypeScript Review Guide

Apply this guide to TypeScript, Node.js services, browser applications, and
TypeScript build or configuration changes. Distinguish compile-time types from
runtime validation because TypeScript types are erased at runtime.

## Code quality, correctness, and performance

- Check strictness settings, `any`, unsafe assertions, non-null assertions,
  index access, widening, discriminated unions, and generic constraints at
  trust boundaries.
- Verify external input with runtime schemas or explicit guards before using
  it as a typed value. Check that validation and transformation preserve the
  intended domain invariants.
- Check promise rejection handling, cancellation/timeouts, event listeners,
  stream backpressure, worker lifecycle, and unhandled errors.
- Check module boundaries, ESM/CommonJS interop, import cycles, generated
  types, declaration output, and compatibility of public APIs.
- Check unnecessary object/array copies, repeated serialization, bundle size,
  synchronous work on Node.js or the browser main thread, and unbounded
  caches/listeners.
- Check tests for runtime-invalid inputs, browser/server differences,
  serialization, time zones, numeric boundaries, and failure paths.

## Security

- Check DOM output, URL construction, template rendering, and HTML insertion
  for XSS. Treat `innerHTML`, `dangerouslySetInnerHTML`, `eval`, `Function`,
  dynamic imports, and string-built scripts as explicit trust boundaries.
- Check prototype pollution, unsafe object merging, path handling, command
  execution, SQL/NoSQL queries, SSRF, redirects, and archive processing in
  Node.js code.
- Verify authentication, authorization, tenant isolation, CSRF, cookie flags,
  origin checks, and server-side enforcement rather than trusting client types
  or hidden UI controls.
- Check secrets in browser bundles, source maps, logs, error payloads,
  environment variables exposed through build tooling, and public config.
- Inspect JSON/URL/form parsing, schema validation, file uploads, and
  deserialization for resource exhaustion and type confusion.
- Review npm/pnpm/yarn dependency, lifecycle-script, lockfile, bundler, and
  source-map changes for supply-chain or accidental exposure risks.
