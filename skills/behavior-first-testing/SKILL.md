---
name: behavior-first-testing
description: Behavior-first web testing with Vitest, Vitest Browser Mode, Playwright, Testing Library, MSW, and TDD. Use when writing or reviewing tests, choosing test boundaries, deciding between browser tests and jsdom, reducing flakiness, or enforcing user-centered assertions.
---

# Behavior-First Testing

Use this skill when the user asks to write, fix, review, or redesign tests for web apps and the work touches UI behavior, Vitest, Playwright, Testing Library, MSW, flakiness, `jsdom`, or test boundaries.

## Core rules

- Test behavior through public interfaces.
- Prefer browser tests for browser behavior.
- Prefer real boundaries over mocked internals.
- Write one failing behavior at a time.
- Keep setup deterministic and cleanup explicit.
- If the repo or user has stricter rules than this skill, follow the stricter rules.

## Workflow

1. Identify the system under test and its public interface.
2. Choose the highest-value boundary that still stays local and reliable.
3. Choose the runtime:
   - Pure deterministic logic or server logic: Vitest in Node.
   - Component or single-page browser behavior: Vitest Browser Mode first.
   - Navigation, auth, multi-page flows, or browser/system seams: Playwright.
   - Do not default to `jsdom`.
4. List the highest-value behaviors to prove.
5. Use a vertical red-green-refactor loop:
   - write one failing behavior test
   - verify it fails for the expected reason
   - implement the minimum change
   - refactor only after green
6. Assert on outcomes the user or caller can observe, not on internal calls.
7. If the test becomes flaky, first question the boundary, waits, cleanup, and runtime choice.

## Practical defaults

- Prefer `getByRole(..., { name })`, then labels, then visible text. Use test IDs only as an escape hatch.
- In Testing Library, prefer `userEvent.setup()` over low-level `fireEvent` for real interactions.
- In Playwright, prefer locators and web-first assertions over CSS/XPath and manual waits.
- In Vitest Browser Mode, lean on `expect.element(...)` instead of hand-rolled polling.
- If the network boundary must be mocked, prefer a shared MSW layer over ad hoc fetch stubs.
- Do not make request payload inspection the main assertion. Make invalid outbound data fail through the boundary behavior instead.
- Only use `jsdom` when a real browser runner is genuinely blocked and call out the tradeoff explicitly.

## When to reach for which tool

- Vitest Node: pure transforms, schema logic, server-only modules, deterministic helpers.
- Vitest Browser Mode: component rendering, form behavior, focus/keyboard/DOM interaction inside one page.
- Playwright: navigation, auth, multi-step workflows, real browser integration seams, production-like smoke coverage.
- MSW: when you need controllable network behavior without rewriting app code or patching `fetch` directly.
- Keep Playwright coverage focused on the highest-value user journeys instead of pushing every edge case into E2E.

See:
- `references/strategy.md`
- `references/runtimes.md`
- `references/queries-and-assertions.md`
- `references/network-and-mocks.md`
- `references/cleanup-and-flakes.md`

## Output expectations

When using this skill for a code change:

- state the chosen test boundary
- state the chosen runtime
- name the first failing behavior
- explain any mocking or no-mocking decision
- call out any flake or cleanup risk
