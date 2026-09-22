# Security Review Checklist

When reviewing code, systematically check the areas that apply. Only report a
vulnerability when the code and its data flow provide evidence for it.

For language and framework-specific security checks, use
`rules/languages/index.md` to select the applicable guides. For mixed-language
changes, load every relevant guide and keep shared concerns separate from
language-specific concerns. If no guide exists, use this checklist and state
that the review used generic guidance.

1. **Inputs and injection**
   - Are untrusted inputs validated for type, size, range, and expected format?
   - Are SQL/NoSQL/LDAP queries, shell commands, templates, and HTML safely
     parameterized or encoded?
   - Are file paths, redirects, URLs, and archive contents protected against
     traversal, SSRF, open redirects, and unsafe file access?

2. **Authentication, authorization, and abuse controls**
   - Is authentication enforced at the correct boundary?
   - Are object-level and role-based permissions checked server-side?
   - Are sessions, tokens, cookies, CSRF protections, rate limits, and
     replay/idempotency behavior appropriate for the operation?

3. **Secrets and sensitive data**
   - Are API keys, tokens, passwords, or private certificates hardcoded,
     logged, committed, or exposed in client-visible responses?
   - Is personal, financial, or tenant data minimized and protected in
     responses, logs, caches, analytics, and error messages?

4. **Parsing, cryptography, and dependencies**
   - Is user-controlled JSON, YAML, XML, serialization, or archive data parsed
     safely without unsafe object construction or resource exhaustion?
   - Are cryptographic primitives, randomness, certificate validation, and
     password storage appropriate for the use case?
   - Do dependency or configuration changes introduce a clear supply-chain or
     insecure-default risk?

5. **Failure and information leakage**
   - Do errors, stack traces, debug endpoints, metrics, or logs disclose
     credentials, internal topology, or sensitive records?
   - Are security failures handled closed-by-default without silently bypassing
     validation or authorization?