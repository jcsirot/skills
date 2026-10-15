# Node.js Review Guide

Apply this guide to TypeScript or JavaScript that executes in Node.js. Confirm
the supported Node.js version and module configuration from the relevant
manifest, runtime settings, and source.

## Code quality, correctness, and performance

- Check ESM/CommonJS interoperability, package `exports`/`imports`, module
  resolution, and compatibility with the supported Node.js version.
- Check event-loop blocking, CPU-heavy work, stream backpressure, unbounded
  buffering, worker ownership, and cleanup of listeners and timers.
- Check promise rejection handling, cancellation/timeouts, process-level error
  behavior, and graceful server or worker shutdown.
- Check filesystem and temporary-file lifecycle, path handling, child-process
  arguments, and resource limits on request parsing and archive processing.
- Review Node-specific dependency, package-script, and lockfile changes for
  runtime compatibility and maintenance risk.

## Security

- Trace untrusted data into SQL/NoSQL queries, shell commands, dynamic code,
  filesystem paths, redirects, archive extraction, and outbound requests.
  Prefer parameterized APIs, argument arrays, and explicit destination or path
  allowlists.
- When the server renders HTML, verify template escaping and output encoding
  for the exact HTML, JavaScript, CSS, and URL contexts.
- For HTTP services, verify server-side authentication, authorization,
  tenant/object ownership, request validation, CSRF/cookie protections where
  applicable, and rate limits on sensitive endpoints.
- Check request body and upload limits, actual file handling, and protection
  against SSRF and unsafe redirects.
- Check secrets in environment/configuration flows, process arguments, logs,
  error responses, and crash reporting.
- Review dependency lifecycle scripts, executable package entry points, and
  registry/source changes for supply-chain exposure.
