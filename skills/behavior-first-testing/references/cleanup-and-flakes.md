# Cleanup And Flakes

Flaky tests are usually a boundary, cleanup, or waiting problem.

## Cleanup

- Prefer disposable helpers that own teardown.
- Use `Symbol.dispose` or `Symbol.asyncDispose` with `using` when the runtime supports it.
- Prefer disposable local infrastructure over half-faked collaborators when behavior crosses that seam.

## Flake handling

- Skip temporarily if needed to contain damage.
- Mitigate the obvious instability.
- Assess the real cause: boundary, runtime, shared state, timing, or cleanup.
- Rewrite if the structure is wrong.
- Throw away a test that no longer gives trustworthy signal.

## Common causes

- shared state between tests
- manual sleeps instead of observable signals
- negative assertions that run too early
- browser behavior tested outside a real browser
- leaked infrastructure or global state
