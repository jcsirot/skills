# Browser TypeScript Review Guide

Apply this guide to TypeScript that executes in a browser. Confirm supported
browsers and the client build configuration before relying on browser APIs or
security policies.

## Code quality, correctness, and performance

- Check DOM event listeners, timers, observers, subscriptions, workers, and
  object URLs for cleanup across component and page lifecycles.
- Check synchronous work on the main thread, rendering and serialization
  costs, unbounded client caches, and cancellation of fetches or other
  asynchronous work when the UI no longer needs it.
- Check browser compatibility, storage behavior, navigation, and error states
  across relevant supported browsers.

## Security

- Check DOM rendering and URL construction for XSS and unsafe navigation.
  Treat `innerHTML`, framework raw-HTML escape hatches, `eval`, `Function`,
  dynamic scripts, and untrusted `postMessage` data as trust boundaries.
- Verify output encoding matches the HTML, JavaScript, CSS, or URL context.
  Check CSP and Trusted Types where the application uses them.
- Check authentication state, origin checks, cookie/CSRF behavior, and
  authorization enforcement at the server; client-side checks are not access
  control.
- Check public bundles, source maps, build-time environment substitution, and
  client-visible configuration for secrets. Review token storage for exposure
  to script injection.
- Check external links and embedded content for opener isolation, safe
  protocols, sandboxing, and unintended data exposure.
