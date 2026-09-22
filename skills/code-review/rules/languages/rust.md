# Rust Review Guide

Apply this guide to Rust code, Cargo manifests, asynchronous runtimes, and FFI
boundaries. Review the safety contract of the actual crate and toolchain rather
than treating every warning or `unsafe` block as a defect.

## Code quality, correctness, and performance

- Check `Option` and `Result` handling at boundaries. Flag `unwrap`, `expect`,
  `panic!`, and ignored results when input or runtime failure can reach them;
  do not flag deliberate invariant checks without examining the invariant.
- Check ownership, borrowing, lifetimes, unnecessary `clone`/allocation,
  collection choice, iterator behavior, and whether an API preserves useful
  zero-copy or streaming behavior.
- In async code, check for locks or non-`Send` work held across `.await`,
  blocking calls on async executors, unbounded channels, cancellation gaps,
  task leaks, and missing shutdown or backpressure.
- Check `Send`/`Sync` assumptions, shared mutable state, lock ordering,
  poisoning behavior, atomics, and data-race prevention at thread boundaries.
- Check `Drop`/RAII cleanup for files, sockets, transactions, child processes,
  guards, and spawned tasks.
- For Cargo changes, inspect feature flags, MSRV/toolchain compatibility,
  build scripts, optional dependencies, and tests run under the relevant
  feature combinations. Use `cargo fmt`, `cargo clippy`, and targeted tests
  when the repository makes them available.

## Security

- Treat every `unsafe` block and FFI wrapper as a boundary with explicit
  safety invariants. Verify pointer validity, lifetimes, aliasing, alignment,
  ownership transfer, initialization, thread-safety, and error cleanup.
- Check `serde` and other deserialization paths for unbounded input, dangerous
  defaults, type confusion, recursive data, and validation after parsing.
- Check SQL, shell commands, filesystem paths, URLs, archive extraction, and
  process spawning for parameterization, traversal, SSRF, injection, and
  resource-exhaustion risks.
- Verify authorization and tenant checks are performed before object access,
  including in handlers, extractors, background tasks, and FFI-facing APIs.
- Check secrets in source, logs, panic messages, debug formatting, environment
  propagation, and serialized error values. Be careful with `Debug` derives
  on credential-bearing types.
- Check cryptographic algorithms, nonce/key handling, constant-time
  comparisons where required, certificate validation, and secure randomness.
- Inspect Cargo dependency, build-script, procedural-macro, and feature
  changes for supply-chain exposure or accidental activation of insecure code.
