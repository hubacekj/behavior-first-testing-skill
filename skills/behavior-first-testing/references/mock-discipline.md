# Mock Discipline

Use this file when deciding whether a mock is acceptable and how to clean it up.

## Preferred stance

- Do not mock internal application collaborators.
- Do not use mocks to prove implementation details.
- Prefer real boundaries, disposable local infrastructure, or higher-level tests.

## When mocking is acceptable

Mocking can be acceptable when the mocked boundary is outside the responsibility of the system under test, for example:

- a third-party API
- a payment provider
- a remote webhook target
- time or randomness

Even then:

- keep mocks in setup
- do not make mock call counts the core behavior proof
- make wrong inputs fail through the boundary behavior, not through mock-inspection assertions

## Mock state management

- clear: remove recorded calls
- reset: remove recorded calls and mock implementations
- restore: remove the mock and restore the original implementation

If the repo uses mocks, prefer automatic mock reset between tests and restore spies after the suite.

If the repo bans mocks, obey the repo and move up the testing boundary instead.

Source basis:

- Epic Web: "The Difference Between Clearing, Resetting, and Restoring Mocks"

