---
name: implement
description: Implement sub-issues from docs/issues using sequential fresh sub-agents, with TDD for behavior and frontend design verification for UI-heavy slices. Use when user wants to implement a feature, run through sub-issues, or build from docs/issues.
---

# Implement

Implement the current feature from `docs/issues/`.

`docs/issues/` is the implementation queue for the current feature branch. Do not read `docs/prd/`, the original ticket, or the original conversation unless a sub-issue explicitly says required context is missing.

Load only:

1. `docs/issues/_context_issue.md`
2. One sub-issue file at a time
3. Targeted code, tests, and docs needed for that sub-issue

## Queue Mode

When the user points to `docs/issues/` or asks to implement the feature:

1. Read `_context_issue.md`.
2. Read only filenames, status, and `Blocked by` sections for sub-issues.
3. Pick the first `todo` sub-issue in implementation order.
4. Start a fresh sequential sub-agent to implement it. Give the sub-agent `_context_issue.md`, the sub-issue file, the TDD rules from this skill, and the targeted context it needs.
5. Mark it done in both `_context_issue.md` and the sub-issue file.
6. Continue to the next sub-issue.

Do not skip implementations silently. If a sub-issue is `HITL`, blocked, ambiguous, or the sub-agent needs a decision/access/action to continue, pause the queue and ask the user for exactly what is needed. Continue only after the user resolves it.

Do not run implementation sub-agents in parallel by default; they share the same branch and can step on each other's files.

## Sub-Issue Loop

For each sub-issue:

1. Read `_context_issue.md` and the selected sub-issue.
2. Load only the `Context to load` targets and nearby code needed to work.
3. Classify the work:
   - **No UI**: use the TDD workflow.
   - **Light UI**: use TDD for behavior, then do lightweight visual/browser checks.
   - **Design-heavy UI**: read [frontend-design.md](frontend-design.md) and [motion-design.md](motion-design.md), then verify visually instead of forcing strict TDD for the visual layer.
4. Have the sub-agent implement the slice end-to-end.
5. Run the narrowest meaningful checks first, then broader checks if appropriate.
6. Refactor only while green.
7. Update status.

## TDD Philosophy

**Core principle**: Tests should verify behavior through public interfaces, not implementation details. Code can change entirely; tests shouldn't.

**Good tests** are integration-style: they exercise real code paths through public APIs. They describe _what_ the system does, not _how_ it does it. A good test reads like a specification - "user can checkout with valid cart" tells you exactly what capability exists. These tests survive refactors because they don't care about internal structure.

**Bad tests** are coupled to implementation. They mock internal collaborators, test private methods, or verify through external means (like querying a database directly instead of using the interface). The warning sign: your test breaks when you refactor, but behavior hasn't changed.

See [tests.md](tests.md) for examples and [mocking.md](mocking.md) for mocking guidelines.

## Anti-Pattern: Horizontal Slices

**DO NOT write all tests first, then all implementation.** This is horizontal slicing.

Correct approach: vertical slices via tracer bullets. One test -> one implementation -> repeat.

```text
WRONG:
  RED:   test1, test2, test3
  GREEN: impl1, impl2, impl3

RIGHT:
  RED->GREEN: test1->impl1
  RED->GREEN: test2->impl2
  RED->GREEN: test3->impl3
```

## TDD Workflow

### 1. Planning

When exploring the codebase, use the project's domain glossary so that test names and interface vocabulary match the project's language, and respect ADRs in the area you're touching.

Before writing code for the current sub-issue:

- [ ] Identify the public behavior to prove
- [ ] Identify opportunities for [deep modules](deep-modules.md)
- [ ] Design interfaces for [testability](interface-design.md)
- [ ] Choose the narrowest useful test/check

Do not ask the user to re-approve every sub-issue in queue mode unless the sub-issue is ambiguous, blocked, HITL, or the sub-agent cannot continue without user input.

### 2. Tracer Bullet

Write ONE test that confirms ONE thing about the system:

```text
RED:   Write test for first behavior -> test fails
GREEN: Write minimal code to pass -> test passes
```

### 3. Incremental Loop

For each remaining behavior:

```text
RED:   Write next test -> fails
GREEN: Minimal code to pass -> passes
```

Rules:

- One test at a time
- Only enough code to pass current test
- Don't anticipate future tests
- Keep tests focused on observable behavior

### 4. Refactor

After tests pass, look for [refactor candidates](refactoring.md). Never refactor while red.

## Frontend Rule

Use TDD for behavior. Use design references for taste. Use browser/screenshot verification for visual correctness.

For frontend slices, still test meaningful behavior: form validation, navigation, persisted state, accessibility-critical flows, and API error handling. Do not write brittle tests for spacing, class names, animation timing, snapshots, or implementation details.

## Done

A sub-issue is done when:

- Acceptance criteria are satisfied
- Relevant tests/checks pass
- UI-heavy work has been visually verified when possible
- Debug/prototype code is removed
- `_context_issue.md` and the sub-issue status are updated
