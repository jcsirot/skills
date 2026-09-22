# Language and Framework Routing

Select guides from changed files, manifests, build files, lockfiles, CI, and
visible dependencies. Load every applicable guide for mixed-language changes.
Prefer repository conventions and verified framework behavior over generic
advice. If no guide matches, use the shared checklists and state that coverage
is generic.

| Signals | Guide |
|---|---|
| `.java`, Maven/Gradle JVM builds, Spring, Quarkus, Jakarta EE | `java.md` |
| `.kt`, Kotlin DSL, Kotlin/JVM, Android, Kotlin Multiplatform | `kotlin.md` |
| `.rs`, `Cargo.toml`, Rust async or FFI | `rust.md` |
| `.ts`, `tsconfig`, Node.js or browser TypeScript | `typescript.md` |
| `.html`, server-rendered templates, HTML components | `html.md` |
| `.css`, Sass/Less, CSS modules, utility stylesheets | `css.md` |

Framework-specific advice is valid only when the framework is visible in the
repository, its dependencies, or its documentation.
