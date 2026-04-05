# Flaky Tests

Use this file when a test is unreliable.

## Principle

A flaky test is a design problem first.

Do not normalize flakiness with arbitrary sleeps, retries, or weaker assertions unless you can justify the tradeoff.

## S.M.A.R.T.

- Skip it temporarily if it is blocking work and you need to contain damage.
- Mitigate the most obvious instability while you investigate.
- Assess the real cause and whether the chosen boundary is wrong.
- Rewrite the test if the original structure cannot be made reliable.
- Throw it away if it no longer provides trustworthy value.

## Common causes

- shared state
- cleanup leaks
- relying on time instead of observable signals
- negative assertions that pass too early
- tests crossing too many unrelated systems
- browser behavior tested in a fake browser environment

Source basis:

- Epic Web: "Be S.M.A.R.T. About Flaky Tests"
- Epic Web: "Writing Tests That Fail"

