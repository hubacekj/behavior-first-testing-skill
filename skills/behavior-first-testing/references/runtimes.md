# Runtimes

Use the runtime that matches the behavior.

## Choose Node Vitest for

- pure logic
- schema validation
- formatting
- server-only modules
- deterministic transforms

## Choose Vitest Browser Mode for

- component behavior
- form interaction inside one page
- DOM, focus, keyboard, and async rendering behavior
- fast feedback in a real browser runtime

## Choose Playwright for

- page-to-page workflows
- navigation
- auth
- uploads, downloads, and browser integrations
- smoke coverage for real user journeys

## `jsdom`

Do not default to `jsdom`.

Use it only when a real browser runner is blocked by a concrete repo/tooling constraint and you accept the tradeoff explicitly.

