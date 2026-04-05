# Queries And Assertions

Prefer queries and assertions that resemble user behavior.

## Query order

1. role + accessible name
2. label text
3. visible text
4. other semantic queries
5. test IDs as an escape hatch

## Query type rules

- `getBy*` for synchronous presence
- `findBy*` for async appearance
- `queryBy*` for absence checks

## Interaction rules

- In Testing Library, prefer `userEvent.setup()` and user interactions over low-level events.
- Use `fireEvent` only when the browser-level interaction you need is not modeled.
- In Playwright, prefer locators over CSS/XPath and prefer web-first assertions over manual sleeps.

## Assertion rules

- Use visibility assertions when user visibility is what matters.
- Use DOM-presence assertions when presence itself matters.
- Negative assertions must wait on the right signal; they can otherwise pass too early.
- Avoid boilerplate assertions that only repeat what setup already guarantees.
