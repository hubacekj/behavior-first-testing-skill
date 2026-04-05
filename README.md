# Behavior-First Testing Skill

A reusable agent skill package for behavior-first testing with Vitest, Vitest Browser Mode, Playwright, and TDD.

This package is built around:

- public-interface testing instead of implementation testing
- browser-first UI testing instead of `jsdom` by default
- one failing behavior at a time
- careful test-boundary selection
- disposable test infrastructure
- flake management that treats flakiness as a design problem

## Install

List the skills in this package:

```bash
npx skills add hubacekj/behavior-first-testing-skill --list
```

Install globally:

```bash
npx skills add hubacekj/behavior-first-testing-skill -g --skill behavior-first-testing -y
```

Install from a local checkout:

```bash
npx skills add /absolute/path/to/behavior-first-testing-skill -g --skill behavior-first-testing -y
```

## Included skill

- `behavior-first-testing`: Use when writing, reviewing, or refactoring tests with Vitest, Vitest Browser Mode, Playwright, mock discipline, flaky test cleanup, or browser-vs-jsdom decisions.

