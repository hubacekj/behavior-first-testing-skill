---
name: behavior-first-testing
description: Behavior-first web testing with Vitest, Vitest Browser Mode, Playwright, Testing Library, MSW, and TDD. Use when writing or reviewing tests for web apps, choosing test boundaries, deciding between browser tests and jsdom, reducing flakiness, or enforcing user-centered assertions.
---

# Behavior-First Testing

Use this skill when the user asks to write, fix, review, or redesign tests for web apps and the work touches UI behavior, Vitest, Playwright, Testing Library, MSW, flakiness, `jsdom`, or test boundaries.

This skill is web-app-first. Node/server tests are in scope only when they support a web app behavior or boundary.

This skill is about authored automated tests and testing strategy. For agent-run browser exploration, manual verification, screenshots, DOM inspection, and interactive reproduction, treat `agent-browser` as the authority and use it alongside this skill when needed.

Keep this skill framework-agnostic. If a repo needs React, TanStack, Remix, or Next-specific testing conventions, add a repo-local supplement instead of bloating this global skill.

## Core rules

- Test behavior through public interfaces.
- Prefer browser tests for browser behavior.
- Prefer real boundaries over mocked internals.
- Write one failing behavior at a time.
- Keep setup deterministic and cleanup explicit.
- Never default to `jsdom`.
- If the repo or user has stricter rules than this skill, follow the stricter rules.

## Workflow

1. Identify the system under test and its public interface.
2. Choose the highest-value boundary that still stays local and reliable.
3. Choose the runtime:
   - Pure deterministic logic or server logic: Vitest in Node.
   - Component or single-page browser behavior: Vitest Browser Mode first.
   - Navigation, auth, multi-page flows, and production-like journey coverage: Playwright.
   - Only use `jsdom` when real browser runners are genuinely blocked and call out the tradeoff.
4. List the highest-value behaviors to prove.
5. For browser-facing work, use `agent-browser` first when live reproduction or DOM inspection will clarify the behavior before you author tests.
6. Use a vertical red-green-refactor loop:
   - write one failing behavior test
   - verify it fails for the expected reason
   - implement the minimum change
   - refactor only after green
7. Assert on outcomes the user or caller can observe, not on internal calls.
8. If the test becomes flaky, first question the boundary, waits, cleanup, and runtime choice.

## Practical defaults

- Prefer `getByRole(..., { name })`, then labels, then visible text. Use test IDs only as an escape hatch.
- In Testing Library, prefer `userEvent.setup()` over low-level `fireEvent` for real interactions.
- In Playwright, prefer locators and web-first assertions over CSS/XPath and manual waits.
- In Vitest Browser Mode, lean on `expect.element(...)` instead of hand-rolled polling.
- If the network boundary must be mocked, prefer a shared MSW layer over ad hoc fetch stubs.
- Do not make request payload inspection the main assertion. Make invalid outbound data fail through the boundary behavior instead.
- Prefer visible assertions when user visibility is what matters.
- Only use `jsdom` when a real browser runner is genuinely blocked and call out the tradeoff explicitly.

## When to reach for which tool

- Vitest Node: pure transforms, schema logic, server-only modules, deterministic helpers.
- Vitest Browser Mode: component rendering, form behavior, focus/keyboard/DOM interaction inside one page.
- Playwright: navigation, auth, a small number of high-value journeys, real browser integration seams, and production-like smoke coverage.
- MSW: when you need controllable network behavior without rewriting app code or patching `fetch` directly.
- `agent-browser`: agent-driven browser execution, exploratory verification, screenshots, DOM inspection, and live repro work. Do not treat it as the source of truth for authored test files.
- Keep Playwright coverage narrow. Do not push every edge case into E2E.

See:
- `references/strategy.md`
- `references/runtimes.md`
- `references/queries-and-assertions.md`
- `references/network-and-mocks.md`
- `references/cleanup-and-flakes.md`

## Output expectations

When using this skill for a code change:

- for non-trivial testing work, state the chosen test boundary
- for non-trivial testing work, state the chosen runtime
- name the first failing behavior
- explain any mocking or no-mocking decision
- call out any flake or cleanup risk
