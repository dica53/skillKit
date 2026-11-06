---
name: principle-testing-code
description: "Apply when writing, changing, or reviewing automated tests. Write the smallest test that pins what the code's users can observe, keep its runtime flat as the suite grows, and check it fails when behavior breaks but survives internal changes."
---

# Testing Code

A test is a claim about what the code does for its users: a caller, an end user, or another service. It earns its place when it fails if that behavior breaks, keeps passing when only the internals change, and costs little to run every time CI does.

Use this guideline to push back on review comments that assert for test coverage.

## Write the minimum test

- **Test risky behavior and contracts,** not every line. Skip states the app cannot reach.
- **One behavior per test,** at the narrowest level that reaches it. Extend the existing test file, fixtures and helpers for that code path before adding a new harness or mock layer.
- **Each case covers a distinct path.** Before adding a case, name the branch or rule only it exercises. Drop cases that another case or another test already covers.

## Assert behavior, not implementation

- **Behavior:** return values, errors that callers branch on, state they can read back, invariants (such as a key that must exist in two tables), and effects on outside systems, including the payload a mocked external service receives.
- **Not implementation:** private helpers, internal call order, intermediate data, which collaborator did the work, and wording that no caller reads, such as exact error messages.
- **Exact values from the requirement.** Pin the exact result, both ends of a range or clamp, the branch that wins, and the default path. Avoid loose bounds, and never derive the expected value from a run of the code or from data the test built itself.
- **Absence needs a pair.** When asserting that something does not happen, add a case where it does, so the test proves it can see it.

## Keep runtime flat

Tests against real services (databases, containers, browsers) multiply with every case and run on every CI job, so their cost grows quietly.

- **Share expensive setup.** Reuse the suite's existing container, service or seeded fixture instead of starting your own.
- **Seed the fewest rows that exercise the behavior.** Generate bulk data in one statement on the server, not row by row from the test.
- **Trim parametrization.** Replace cross products with the cases that hit distinct paths. A value the code only passes through needs one case, not one per variant.
- **No waiting on the clock.** No sleeps, polling with delays, or reliance on today's date; pin dates in the past.
- **Measure per test, not per suite.** Use the runner's duration report, and compare the slow tests before and after, since suite totals are noisy. Note where the file lands in CI sharding, because one slow file can set a whole job's time.

## Check

For each new or changed test, name an edit that breaks the behavior (or reverts the line under test) and confirm the test would fail. Then name an internal change that keeps behavior and confirm the test still passes. After trimming cases or data, confirm the remaining cases still catch that break. Rewrite or delete tests that fail either check. Reason through this; rerun with the code reverted only when asked.
