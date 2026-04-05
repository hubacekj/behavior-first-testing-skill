# Disposable Infrastructure

Use this file when a test needs real setup and cleanup.

## Principle

Collocate setup and cleanup so cleanup is hard to forget.

Use disposable objects for:

- local web servers
- mail sinks
- Redis containers or temporary Redis processes
- temp directories
- filesystem fixtures
- background workers

## Pattern

- Construct the resource in a helper.
- Attach cleanup with `Symbol.dispose` or `Symbol.asyncDispose`.
- Consume it with `using` / `await using`.

This is especially valuable in test suites because it keeps tests self-contained and prevents leaked state across runs.

## Guidance

- Prefer disposable helpers over `beforeAll` plus `afterAll` sprawl.
- If the runtime or repo cannot use `using`, preserve the same ownership model with explicit teardown helpers.
- Real infrastructure is preferable to fake infrastructure when the behavior under test crosses that boundary.

Source basis:

- Epic Web: "Better Test Setup with Disposable Objects"

