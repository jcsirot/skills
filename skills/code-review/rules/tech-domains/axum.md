# Axum Review Guide

Apply this guide when the changed Rust code uses Axum. Load `tokio.md` as well
because Axum runs on Tokio. Confirm Axum, Tower, and `tower-http` versions and
enabled features before relying on middleware or extractor behavior.

## Code quality, correctness, and performance

- Trace router composition, nested routes, fallback handlers, and middleware
  layer order. Ensure authentication, tracing, timeouts, and error mapping
  cover every intended route.
- Check handler extractor order and rejection behavior. Verify body-consuming
  extractors are not used incompatibly and failures do not become success-
  shaped defaults.
- Validate request data at the boundary, enforce body and upload limits, and
  avoid expensive synchronous work in async handlers.
- Check shared application state for safe ownership and concurrency, and
  ensure graceful shutdown stops serving and background tasks coherently.
- Test routing, middleware, extractor failures, and authorization at the
  router boundary, not only through isolated handler functions.

## Security

- Verify every route, fallback, and nested router has the intended
  authentication and authorization. Check object-level and tenant ownership
  before returning or mutating resources.
- Check request validation, body limits, multipart handling, and extractor
  errors for injection, resource exhaustion, and information leakage.
- Review cookie/session and CSRF behavior for browser-authenticated endpoints.
  Configure CORS for the required origins and methods; do not treat CORS as
  authorization.
- Check middleware ordering for security headers, request IDs, rate limits,
  authentication, and error handling. Verify sensitive errors do not expose
  internal details.
