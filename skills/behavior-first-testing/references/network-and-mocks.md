# Network And Mocks

Prefer real boundaries. When you must control the network boundary, do it deliberately.

## Mock rules

- Do not mock internal collaborators to make assertions easier.
- Do not make request inspection the main proof of behavior.
- Keep mocks in setup, not in expectations.
- If the repo bans mocks, obey the repo and move the test boundary up.

## MSW rules

- Prefer MSW over ad hoc fetch stubs when mocking the network boundary.
- Treat API mocking as a standalone layer that can be reused across development, integration tests, and end-to-end tests.
- Make wrong outbound data fail through the mocked boundary behavior so the user-visible result changes.
- Prefer strict unhandled-request handling in test setup so unexpected network calls fail fast.

## Mock state

- clear: remove call history
- reset: remove call history and mock implementations
- restore: remove the mock and restore the original implementation
