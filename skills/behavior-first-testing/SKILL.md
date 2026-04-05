---
name: behavior-first-testing
description: Behavior-first testing with Vitest, Vitest Browser Mode, Playwright, disposable test infrastructure, and TDD. Use when writing or reviewing tests, deciding between browser tests and jsdom, setting test boundaries, reducing flakiness, avoiding implementation-detail assertions, or discussing mocks.
---

# Behavior-First Testing

Use this skill when the user asks to write, fix, review, or redesign tests and the work touches UI behavior, Vitest, Playwright, mocking, flakiness, `jsdom`, or test boundaries.

## Core stance

- Test behavior through public interfaces.
- Prefer browser tests for browser behavior.
- Prefer real boundaries over mocked internals.
- Write one failing behavior at a time.
- Keep setup deterministic and cleanup explicit.
- If the repo or user has stricter rules than this skill, follow the stricter rules.

## Workflow

1. Identify the system under test and its public interface.
2. Choose the narrowest boundary that still proves the intended behavior.
3. Choose the runtime:
   - Pure deterministic logic: Vitest in Node.
   - Browser UI behavior: Vitest Browser Mode first.
   - Cross-page flows, navigation, real forms, or real integration seams: Playwright.
   - Do not default to `jsdom`.
4. List the highest-value behaviors to prove.
5. Use a vertical red-green-refactor loop:
   - write one failing behavior test
   - implement the minimum change
   - refactor only after green
6. Assert on outcomes the user or caller can observe, not on internal calls.
7. If a test flakes, treat that as a design problem and use the S.M.A.R.T. rubric in `references/flaky-tests.md`.

## Decision rules

### Choosing a test boundary

- Favor the highest boundary that is still fast and local enough to be useful.
- Do not verify implementation details like helper calls, internal function dispatch, or raw request assertions.
- If payload correctness matters, encode it into the boundary setup so the observable outcome changes when the payload is wrong.
- When a module is hard to test without invasive mocks, first consider changing the module design.

See:
- `references/test-boundaries.md`
- `references/design-for-testability.md`

### Choosing browser vs Node vs jsdom

- Browser behavior belongs in a real browser runtime.
- Use Vitest Browser Mode for component-level browser behavior when you want fast feedback.
- Use Playwright for full-user journeys or when multiple browser subsystems matter together.
- Use Node Vitest for server-side or pure logic modules.
- Only use `jsdom` when there is a concrete constraint that blocks browser-mode or Playwright and the tradeoff is explicit.

See:
- `references/browser-testing.md`

### Mocking

- Do not mock internal collaborators to make assertions easier.
- Do not assert on mocked requests as the primary proof of behavior.
- Prefer real collaborators or disposable local infrastructure when practical.
- If you must mock an external boundary, keep the mock in setup, not in expectations.
- Reset mock state intentionally:
  - clear: remove call history
  - reset: remove call history and mock implementations
  - restore: remove the mock itself and restore the original implementation

See:
- `references/mock-discipline.md`

## Assertion rules

- For visible presence in UI tests, prefer visibility assertions.
- For absence, use absence assertions that reflect the user-visible intent.
- Use inverse assertions carefully; avoid patterns that can pass immediately without proving anything.
- Avoid boilerplate assertions that only restate setup.

See:
- `references/assertion-guidelines.md`

## Test setup

- Keep tests isolated and disposable.
- Prefer utilities that own their cleanup via `Symbol.dispose` / `Symbol.asyncDispose` and `using`.
- Use local disposable infrastructure for integrations when needed: Redis, mail sink, temp directories, local servers.
- Do not let cleanup depend on developer discipline alone.

See:
- `references/disposable-infrastructure.md`

## Vitest defaults to lean into

- Reuse the real Vite pipeline where possible.
- Keep APIs explicit instead of enabling global `test`/`expect` by default unless the repo already standardizes on globals.
- Preserve test isolation.
- Be aware that file-level parallelism and sequential tests within a file are defaults with tradeoffs.
- In Browser Mode, use retryable element assertions instead of hand-rolled polling.

See:
- `references/vitest-defaults.md`

## Output expectations

When using this skill for a code change:

- state the chosen test boundary
- state the chosen runtime
- name the first failing behavior
- explain any mocking or no-mocking decision
- call out any flake or cleanup risk

