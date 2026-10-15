# Language and Framework Routing

Select guides from changed files, manifests, build files, lockfiles, CI, and
visible dependencies. Load every applicable guide for mixed-language changes.
For Java, load the generic guide for Java/JVM changes and add a framework guide
only when its specific marker is present in the relevant `pom.xml` or parent
POM. Gradle evidence alone does not trigger these framework guides. If the POM
is unavailable, do not infer a Spring Boot or Quarkus guide from Java source
alone; use `java.md` and state that framework-specific configuration could not
be verified. Prefer repository conventions and verified framework behavior
over generic advice. If no guide matches, use the shared checklists and state
that coverage is generic.

| Signals | Guide |
|---|---|
| `.java`, Maven/Gradle JVM build files, or Jakarta EE APIs | `java.md` |
| Spring Boot or Quarkus marker in Maven `pom.xml` (details below) | Matching framework guide in addition to `java.md` |
| `.kt`, Kotlin DSL, Kotlin/JVM, Android, Kotlin Multiplatform | `kotlin.md` |
| `.rs`, `Cargo.toml`, Rust async or FFI | `rust.md` |
| `.ts`, `tsconfig` | `typescript.md` |
| Node.js TypeScript runtime (details below) | `nodejs.md` in addition to `typescript.md` |
| Browser TypeScript runtime (details below) | `browser.md` in addition to `typescript.md` |
| Tokio runtime (details below) | `tokio.md` in addition to `rust.md` |
| Axum crate (details below) | `axum.md`, `tokio.md`, and `rust.md` |
| REST API endpoints, contracts, or client behavior (details below) | `rest-api.md` in addition to applicable language/runtime guides |
| `.html`, server-rendered templates, HTML components | `html.md` |
| `.css`, Sass/Less, CSS modules, utility stylesheets | `css.md` |

## Java framework markers in Maven

Load `spring-boot.md` in addition to `java.md` when the relevant `pom.xml` or
parent POM contains a Spring Boot parent (`org.springframework.boot:
spring-boot-starter-parent`), imported BOM
(`org.springframework.boot:spring-boot-dependencies`), dependency with group
`org.springframework.boot` and artifact `spring-boot`, `spring-boot-starter`,
or `spring-boot-starter-*`, or the
`org.springframework.boot:spring-boot-maven-plugin`.

Load `quarkus.md` in addition to `java.md` when the relevant `pom.xml` or parent
POM contains the Quarkus platform BOM
(`io.quarkus.platform:quarkus-bom` or `io.quarkus:quarkus-bom`), the
`io.quarkus:quarkus-maven-plugin`, or a Quarkus extension with group
`io.quarkus` and artifact `quarkus-*`. If both frameworks are detected, load
both guides.

For languages other than Java, select framework advice only when the framework
is visible in the repository, its dependencies, or its documentation. For Java,
the Spring Boot and Quarkus guides follow the Maven-only markers above.

## TypeScript runtime markers

Load `nodejs.md` when the changed TypeScript runs in Node.js, evidenced by
Node.js built-in imports/APIs, a server-side entry point, a Node.js runtime
configuration, or a server framework dependency used by the changed code. Do
not use `@types/node` or a build-tool dependency alone as proof that the
changed code runs in Node.js.

Load `browser.md` when the changed TypeScript runs in a browser, evidenced by
DOM/Web APIs, browser entry points, or client-side application code. In a
full-stack project, load both runtime guides only when the reviewed change
touches both environments or their boundary.

## Rust runtime and web-framework markers

Load `tokio.md` when `tokio` is a direct or workspace dependency in the
relevant `Cargo.toml`, or the changed code directly uses Tokio APIs. Do not
trigger it from an unrelated transitive dependency alone.

Load `axum.md` when `axum` is a direct/workspace dependency or the changed code
uses Axum APIs. Axum changes also load `tokio.md` because Axum's runtime model
is Tokio-based. For workspace dependencies, inspect the workspace manifest and
the relevant crate manifest.

## REST API markers

Load `rest-api.md` alongside the applicable language and runtime guides when
the change adds or modifies REST endpoints, HTTP resource behavior, an API
contract or OpenAPI description, or client code whose behavior depends on a
REST contract. Do not load it for unrelated HTTP transport such as static
asset delivery or telemetry.
