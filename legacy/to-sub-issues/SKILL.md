---
name: to-sub-issues
description: Break a ticket, issue, PRD, or large implementation brief into independently-grabbable sub-issues using tracer-bullet vertical slices sized for 100k-token agent contexts. Use when user wants to split a feature ticket into sub-issues or implementation tickets.
---

# To Sub-Issues

Break a ticket, issue, PRD, or implementation brief into independently-grabbable sub-issues using vertical slices (tracer bullets).

Published sub-issues live directly in `docs/issues/`.

`docs/issues/` represents the current feature branch's implementation queue. Do not create a feature subdirectory inside it.

Each sub-issue should be small enough for an agent to implement with roughly 100k tokens of useful context.

## Process

### 1. Gather context

Work from whatever is already in the conversation context. If the user passes or pastes a ticket, issue, PRD path, name, or URL, use that as the source of truth.

Source priority:

1. The ticket, issue, or brief given by the user in the current request
2. A specific PRD path/name given by the user
3. A relevant PRD in `docs/prd/`, only if present and unambiguous

If no source is provided and no unambiguous PRD exists, ask the developer to provide the ticket or brief.

### 2. Explore the codebase (optional)

If you have not already explored the codebase, do so to understand the current state of the code. Issue titles and descriptions should use the project's domain glossary vocabulary, and respect ADRs in the area you're touching.

Explore only enough to size the sub-issues and identify relevant context. Do not make implementation depend on reading the original PRD or the entire repo.

### 3. Draft vertical slices

Break the source into **tracer bullet** sub-issues. Each sub-issue is a thin vertical slice that cuts through ALL required integration layers end-to-end, NOT a horizontal slice of one layer.

Slices may be `HITL` or `AFK`. HITL slices require human interaction, such as an architectural decision or a design review. AFK slices can be implemented and merged without human interaction. Prefer AFK over HITL where possible.

<vertical-slice-rules>
- Each slice delivers a narrow but COMPLETE path through every required layer
- A completed slice is demoable or verifiable on its own
- Prefer many thin slices over few thick ones
- Avoid slices that require more than ~100k tokens of useful context
- Sub-issues must be implementable from `docs/issues/_context_issue.md`, their own file, and targeted code context
</vertical-slice-rules>

### 4. Quiz the user

Present the proposed breakdown as a numbered list. For each slice, show:

- **Title**: short descriptive name
- **Type**: HITL / AFK
- **Blocked by**: which other slices (if any) must complete first
- **Source coverage**: which source sections, user stories, requirements, or acceptance criteria this addresses
- **Context**: the minimum repo areas or docs a future agent should load

Ask the user:

- Does the granularity feel right? (too coarse / too fine)
- Are the dependency relationships correct?
- Should any slices be merged or split further?
- Are the correct slices marked as HITL and AFK?

Iterate until the user approves the breakdown.

### 5. Write the sub-issues

Create `docs/issues/` if needed.

First write `docs/issues/_context_issue.md`. This file contains the shared source context needed by all sub-issues, so implementation never has to read the original ticket, PRD, or conversation.

Then write one markdown file per approved slice directly under `docs/issues/`.

Publish sub-issues in dependency order (blockers first). Prefix filenames with dependency order:

```text
docs/issues/_context_issue.md
docs/issues/001-short-title.md
docs/issues/002-short-title.md
```

Use the context template and issue body template below.

<context-template>

# Context Issue

## Source

Reference or paste a concise summary of the original ticket, issue, PRD, or brief used to create these sub-issues.

## Product Context

Shared product goal, user problem, constraints, and agreed tradeoffs.

## Technical Context

Shared architecture, modules, APIs, data model notes, and integration points that apply across multiple sub-issues.

## Shared Decisions

Decisions that apply to all sub-issues.

## Global Non-Goals

Things no sub-issue should implement.

## Implementation Order

- [ ] `001-short-title.md`
- [ ] `002-short-title.md`

</context-template>

<issue-template>

## Status

todo

## Type

AFK or HITL.

## Source

A reference to `docs/issues/_context_issue.md`.

## What to build

A concise description of this vertical slice. Describe the end-to-end behavior, not layer-by-layer implementation.

Avoid specific file paths or code snippets — they go stale fast. Exception: if a prototype produced a snippet that encodes a decision more precisely than prose can (state machine, reducer, schema, type shape), inline it here and note briefly that it came from a prototype. Trim to the decision-rich parts — not a working demo, just the important bits.

## Context to load

The minimum slice-specific context a future agent should load in addition to `docs/issues/_context_issue.md`.

## Acceptance criteria

- [ ] Criterion 1
- [ ] Criterion 2
- [ ] Criterion 3

## Blocked by

- A reference to the blocking sub-issue (if any)

Or "None - can start immediately" if no blockers.

</issue-template>

Do NOT close or modify the source PRD, ticket, or issue.
Do NOT require future implementation agents to read the original PRD, ticket, or conversation.
