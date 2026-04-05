# Assertion Guidelines

Use this file when writing UI assertions.

## Presence vs visibility

- Use visibility assertions when the user should actually be able to see the thing.
- Use in-document assertions when DOM presence itself matters, not visibility.

In browser/UI tests, presence usually means visibility, so prefer visibility assertions there.

## Absence and inverse assertions

- Use inverse assertions intentionally.
- Negative assertions can pass too easily if they run before the UI has had a chance to change.
- When proving that something should not happen, make sure the test drives the relevant action and waits on the correct signal.

## Avoid empty assertions

Do not add assertions that only repeat what setup already guarantees.

Examples of low-value assertions:

- asserting an element exists right after a helper that already throws if it cannot find it
- asserting that a mocked request happened when the user-facing result already proves the flow

Source basis:

- Epic Web: "toBeVisible() or toBeInTheDocument()"
- Epic Web: "Inverse Assertions"

