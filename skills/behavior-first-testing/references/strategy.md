# Strategy

Start from the behavior, not the implementation.

## Boundary rules

- Pick the highest boundary that proves the behavior without pulling in unrelated failure modes.
- Prefer public interfaces over internal calls, helper functions, and raw request assertions.
- If a module is painful to test without invasive setup, first improve the module boundary.

## TDD rules

- One failing behavior at a time.
- Minimal code to go green.
- Refactor only after green.
- Do not batch speculative tests horizontally.

## Design rules

- Small interface, deep implementation.
- Side effects near the edge.
- Tests should survive internal refactors that preserve behavior.

