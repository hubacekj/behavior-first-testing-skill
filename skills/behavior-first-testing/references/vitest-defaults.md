# Vitest Defaults

Use this file when you need to choose or explain Vitest defaults.

## Favor the defaults when they help test quality

- Vitest runs modern ESM, TypeScript, and JSX without extra adapters.
- Vitest reuses Vite configuration, which keeps the test transformation pipeline close to the app pipeline.
- Vitest keeps `test` and `expect` explicit by default instead of magical globals.
- Vitest isolates test files in separate workers by default.
- Vitest runs test files in parallel by default.
- Vitest runs tests within a single file sequentially by default.
- In Browser Mode, `expect.element(...)` retries like a locator-based browser assertion instead of forcing manual polling.

## Practical guidance

- Do not turn on globals unless the repo already standardizes on them.
- Treat file isolation as a flake-reduction default, not just a convenience.
- If a file becomes a sequential bottleneck, first split the file by behavior before reaching for broad concurrency.
- For browser behavior, prefer Vitest Browser Mode over `jsdom`.

Source basis:

- Epic Web: "Incredible Vitest Defaults"

