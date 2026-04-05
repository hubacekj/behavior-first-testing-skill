# Browser Testing

Use this file when deciding between Browser Mode, Playwright, Node, and `jsdom`.

## Default rule

If the behavior depends on a browser, test it in a browser.

## Runtime choice

- Node Vitest:
  - pure logic
  - server logic
  - deterministic transforms
- Vitest Browser Mode:
  - component behavior
  - form behavior inside one page
  - DOM, layout, focus, and async element interaction
- Playwright:
  - page-to-page flows
  - navigation
  - auth
  - real browser integration seams

## `jsdom`

Do not default to `jsdom`.

Only use it when:

- the project already depends on it heavily and migration is out of scope, or
- a specific toolchain constraint blocks browser testing for a narrow case

If you use it, call out the tradeoff explicitly.

Source basis:

- Epic Web: "Why I Won't Use JSDOM"
- Epic Web: "Incredible Vitest Defaults"

