# Test Boundaries

Use this file when choosing what the test should include and exclude.

## Core rule

A boundary is where you stop testing your code and start assuming something else works.

Choose a boundary that:

- proves the behavior you care about
- keeps the test self-contained
- does not drag in unrelated failure modes

## Heuristics

- Prefer public interfaces over internals.
- Prefer one meaningful boundary over many tiny mocks.
- If the behavior is user-visible, the test should usually cross the UI boundary.
- If the behavior is pure logic, the boundary can be the function/module API.
- If the behavior depends on external services, either:
  - use a disposable local substitute, or
  - draw the boundary at the network edge and make the mock strict enough that wrong outbound behavior changes the visible outcome

## Request assertions

Do not make raw request assertions the main expectation.

Instead:

- validate outbound data in the mock/setup layer
- return success only for valid payloads
- assert on the resulting visible or public outcome

That keeps expectations focused on behavior while still making malformed requests fail the test.

Source basis:

- Epic Web: "Do NOT Assert on Requests"
- Epic Web: "What Is a Test Boundary"

