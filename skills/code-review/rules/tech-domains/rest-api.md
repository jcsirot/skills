# REST API Review Guide

Apply this guide to REST API producers, contracts, and clients when a change
affects HTTP resource semantics or compatibility. Use it alongside the
applicable language and framework guides, not as a replacement for them.

## Resource and HTTP semantics

- Check that routes and representations expose stable resource concepts.
  Verify `GET`/`HEAD` do not mutate state, `PUT`/`DELETE` preserve idempotency,
  and `POST`/`PATCH` retry behavior is explicitly designed and documented.
- Confirm response status codes describe the actual outcome. Check cases such
  as `201` creation and its `Location`, `202` asynchronous processing, `204`
  with no response content, validation failure, and conflict; avoid
  success-shaped error responses.
- Check request and response media types, content negotiation, serialization,
  and relevant headers. Ensure cache directives do not expose sensitive or
  user-specific data to shared caches.
- Check pagination, filtering, sorting, and batch operations for documented
  behavior, bounded work, and stable results. Validate limits and reject or
  constrain unbounded requests.
- For concurrent updates, verify that lost-update protection or other
  concurrency semantics are appropriate and documented, for example with
  entity tags and conditional requests where useful.

## Contract and compatibility

- Validate path, query, header, and body inputs at the API boundary. Check
  schema constraints, normalization, unsupported values, and request-size
  limits against the contract.
- Compare implementation behavior with OpenAPI or other published contracts.
  Ensure response schemas, status codes, media types, authentication
  requirements, and error responses are accurate.
- Check changes to fields, enum values, defaults, nullability, identifiers,
  pagination, and status codes for compatibility with existing clients.
  Confirm versioning, deprecation, and rollout behavior when compatibility
  cannot be preserved.
- Verify clients handle documented status codes and content types, including
  errors, timeouts, retries, and unknown extension fields without assuming
  every response is a successful JSON representation.

## Problem Details for HTTP APIs

When an API uses the Problem Details format, review it against
[RFC 9457](https://www.rfc-editor.org/rfc/rfc9457) (which obsoletes RFC 7807):

- Use `application/problem+json` for JSON or `application/problem+xml` when
  XML is part of the API contract, following documented content negotiation.
  Keep the schema consistent across the API. Use `type` as the stable
  problem-type identifier (`about:blank` for a generic problem); keep `title`
  concise and stable for that type except for localization, and use `detail`
  for safe, occurrence-specific information. Use `instance` to identify a
  specific occurrence where useful. Define and document extension members
  without changing the meaning of standard members.
- Treat the HTTP response status as authoritative. When a `status` member is
  included, treat it as advisory and ensure it agrees with the actual response
  status. Never expose stack traces, SQL, credentials, internal topology, or
  sensitive data in problem details.
- Ensure clients can process the media type and stable problem type without
  depending on human-readable `detail` text or failing on unknown extensions.
- Do not force Problem Details onto successful resource representations or
  errors that are better represented by an existing domain response. Preserve
  compatibility when introducing the format to an existing API.

## Security and testing

- Verify authentication and object-level authorization for each operation,
  including tenant ownership, not just route-level access. Apply the shared
  security checklist for CSRF, CORS, rate limiting, injection, SSRF, and
  sensitive-data handling where relevant.
- Check request-body and upload limits, safe content types, and error responses
  for resource exhaustion and information leakage.
- Test contract-relevant success and error statuses, invalid and boundary
  inputs, authorization failures, pagination limits, retry/idempotency
  behavior, and Problem Details media type and schema when used.
