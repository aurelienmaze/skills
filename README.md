# Aurelien Maze Skills

Agent skills for turning a blurry idea into implementation-ready work, then shipping it slice by slice.

The workflow is intentionally small:

```text
grill-me
  -> to-prd
  -> to-sub-issues
  -> implement

diagnose / refactor-codebase are used when the work breaks or the architecture starts fighting back.
```

## Install

Install every skill in this repo:

```bash
npx skills@latest add aurelienmaze/skills
```

## Workflow

### 1. Explore the idea

Use [`grill-me`](./grill-me/SKILL.md) to stress-test a plan before writing specs or code. It asks one question at a time and explores the codebase when the answer is discoverable there.

### 2. Create a PRD / issue

Use [`to-prd`](./to-prd/SKILL.md) to turn the conversation into a durable PRD or large issue.

PRDs are written to:

```text
docs/prd/<specific-feature-slug>.md
```

This phase may happen from `main` and may produce several PRDs, so filenames should be specific.

### 3. Split into sub-issues

Use [`to-sub-issues`](./to-sub-issues/SKILL.md) to split a ticket, issue, PRD, or pasted brief into tracer-bullet vertical slices.

Sub-issues are written directly to:

```text
docs/issues/
```

`docs/issues/` represents the current feature branch's implementation queue. It contains:

```text
docs/issues/_context_issue.md
docs/issues/001-first-slice.md
docs/issues/002-second-slice.md
```

`_context_issue.md` holds shared context so implementation agents do not need to read the original PRD, ticket, or conversation.

### 4. Implement

Use [`implement`](./implement/SKILL.md) to execute the sub-issues in order.

`implement` uses fresh sequential sub-agents for sub-issues, gives each one only the needed context, applies TDD for testable behavior, and loads the frontend design references only for UI-heavy slices.

## Skills

- [`grill-me`](./grill-me/SKILL.md) — Interview the user relentlessly about a plan or design until reaching shared understanding.
- [`to-prd`](./to-prd/SKILL.md) — Turn the current conversation context into a PRD that can be reused as a large issue or implementation brief.
- [`to-sub-issues`](./to-sub-issues/SKILL.md) — Break a feature ticket into implementation-ready vertical slices.
- [`implement`](./implement/SKILL.md) — Implement `docs/issues` sub-issues with TDD, sequential sub-agents, and frontend design verification.
- [`frontend`](./frontend/SKILL.md) — Implement frontend/UI work using the bundled design taste and motion design references.
- [`talk`](./talk/SKILL.md) — Discussion-only mode for questions, reasoning, and exploration without changing project state.
- [`diagnose`](./diagnose/SKILL.md) — Disciplined diagnosis loop for hard bugs and performance regressions.
- [`refactor-codebase`](./refactor-codebase/SKILL.md) — Find deepening opportunities that make a codebase more testable and agent-navigable.

## Conventions

- `docs/prd/` is for PRDs and large feature issues.
- `docs/issues/` is for the active feature branch's implementation queue.
- Sub-issues should be vertical slices, not layer-by-layer tasks.
- `implement` should not rely on the original PRD once sub-issues exist.
- UI-heavy implementation slices may load the bundled frontend and motion design references.
- `frontend` loads those same design and motion references directly for standalone UI work.

## Attribution

These skills adapt material from:

- Matt Pocock's MIT-licensed [`mattpocock/skills`](https://github.com/mattpocock/skills)
- Leonxlnx's MIT-licensed [`taste-skill`](https://github.com/Leonxlnx/taste-skill)
- Emil Kowalski's public design engineering material at [animations.dev](https://animations.dev/)
