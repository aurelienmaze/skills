---
name: to-prd
description: Turn the current conversation context into a PRD that can be reused as a large issue or implementation brief. Use when user wants to create a PRD, turn a grilling session into a spec, or prepare a feature for issue breakdown.
---

This skill takes the current conversation context and codebase understanding and produces a PRD. Do NOT interview the user — just synthesize what you already know.

Always write the PRD as markdown under `docs/prd/<specific-feature-slug>.md`. Create `docs/prd/` if it does not exist.

Choose a specific feature slug. The PRD phase may create several PRDs or tickets from the main branch, so avoid generic names like `feature.md`, `ticket.md`, or `prd.md`.

The PRD is a durable handoff document, not a chat summary. Another developer or agent should be able to read it later, without the original conversation, and break it into implementation issues.

## Process

1. Explore the repo to understand the current state of the codebase, if you haven't already. Use the project's domain glossary vocabulary throughout the PRD, and respect any ADRs in the area you're touching.

2. Sketch out the major modules you will need to build or modify to complete the implementation. Actively look for opportunities to extract deep modules that can be tested in isolation.

A deep module (as opposed to a shallow module) is one which encapsulates a lot of functionality in a simple, testable interface which rarely changes.

Check with the user that these modules match their expectations. Check with the user which modules they want tests written for.

3. Write the PRD using the template below, then save it to `docs/prd/<specific-feature-slug>.md`. The result should be copy-pastable into GitHub Issues, Linear, Jira, or another issue tracker without rewriting.

<prd-template>

# <Feature / Project Name>

## Summary

A short, concrete description of what will be built and why it matters.

## Source Context

Summarize the context this PRD comes from:

- User request or goal
- Relevant conclusions from the grilling/design discussion
- Existing product or codebase behavior this builds on
- Constraints, preferences, or tradeoffs already agreed

Do not write "the user said" repeatedly. Convert the conversation into stable project language.

## Problem

Describe the problem from the user's perspective. Include the current pain, missing capability, or ambiguity this work resolves.

## Desired Outcome

Describe the end state in product terms. Be specific enough that someone can tell whether the work succeeded.

## Scope

List what is included in this PRD.

## Non-Goals

List what is explicitly out of scope, including tempting adjacent work that should not be done as part of this PRD.

## User Stories

Write an extensive numbered list of user stories. Each story should use:

1. As an <actor>, I want <capability>, so that <benefit>.

Cover primary flows, edge cases, admin/developer needs when relevant, error states, and handoff needs for future agents.

## Functional Requirements

List concrete behavior the implementation must provide. Use checkboxes so this section can become issue acceptance criteria later.

- [ ] Requirement 1
- [ ] Requirement 2
- [ ] Requirement 3

## UX / Interaction Notes

Describe user-facing flows, states, empty states, loading states, validation, copy requirements, and interaction details. If the work has no UI, write "No direct user-facing UI."

## Technical Plan

Describe the likely implementation approach at the module level. Include:

- Modules that will be built or modified
- Interfaces that may need to change
- Data model, schema, or persistence changes
- API contracts or integration points
- Background jobs, side effects, or operational concerns

Do not overfit to specific file paths unless the codebase already has a clear canonical location that matters for implementation.

## Architectural Decisions

List decisions already made and the reasoning behind them. Include tradeoffs and rejected alternatives when they matter.

Exception: if a prototype produced a snippet that encodes a decision more precisely than prose can (state machine, reducer, schema, type shape), inline only the decision-rich part and note that it came from a prototype.

## Testing Strategy

Describe how this should be tested. Include:

- Critical behaviors to cover first
- Recommended test level (unit, integration, e2e, visual, manual)
- Existing test patterns in the repo to follow
- What should be tested through public behavior rather than implementation details

## Acceptance Criteria

Write a concise checklist that marks the PRD as complete.

- [ ] Criterion 1
- [ ] Criterion 2
- [ ] Criterion 3

## Open Questions

List unresolved questions. If there are none, write "None."

## Handoff Notes

Add anything a future developer or agent needs before breaking this PRD into sub-issues: context limits, risky areas, dependency ordering, suggested first slice, or parts that require human review.

</prd-template>
