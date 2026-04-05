# Design For Testability

Use this file when the code is hard to test without invasive setup.

## Principle

Good code is easier to test because it offers a small, meaningful public interface and hides complexity behind it.

## Heuristics

- Prefer deep modules with simple interfaces.
- Keep side effects near the edge.
- Separate decision-making from environment wiring when it improves clarity.
- Make things easy to use and hard to misuse.
- If a test needs to reach inside the module, the module boundary may be wrong.

## TDD overlay

Use a vertical tracer-bullet loop:

1. choose one public behavior
2. write one failing test
3. implement the minimum
4. refactor only after green

Do not write a horizontal batch of speculative tests before the code teaches you where the real seams are.

Source basis:

- Epic Web: "Good Code, Testable Code"
- local `tdd` skill
