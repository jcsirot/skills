# Tokio Review Guide

Apply this guide when the changed Rust code directly uses Tokio. Confirm the
Tokio version and enabled Cargo features before relying on runtime behavior.

## Code quality, correctness, and performance

- Check runtime construction and feature selection (`rt`, `rt-multi-thread`,
  `macros`, `time`, and `sync`) against actual use and deployment constraints.
- Track spawned tasks and their `JoinHandle`s. Check panic/error propagation,
  detached-task behavior, ownership, cancellation, and shutdown.
- Check `select!` and timeout paths for cancellation safety; dropping a future
  may leave partial work or lose progress.
- Keep blocking or CPU-intensive work off async worker threads. Use bounded
  blocking capacity and backpressure when offloading is necessary.
- Prefer bounded channels and check queue capacity, send failure, and
  backpressure. Verify shared state and lock scope; avoid holding synchronous
  locks across `.await`.
- Check signal handling and graceful shutdown so tasks, connections, and
  background work have an explicit stop path.
- Use deterministic time controls or paused-time tests for timer behavior
  instead of brittle sleeps where the test utilities support them.
