# Aurelien Maze Skills

Agent skills for talking a problem through, building UI that feels right, and shipping a task to an open PR.

```text
talk           -> think it through, no changes
ship           -> implement, review with subagents, open the PR and a preview
better-design  -> design, motion and interaction rules used by ship and any UI work
```

## Install

```bash
npx skills@latest add aurelienmaze/skills
```

## Skills

- [`talk`](./talk/SKILL.md): Discussion-only mode. Ask questions, reason through options and explore an idea without modifying files or project state. Invoke with `/talk`.
- [`ship`](./ship/SKILL.md): Take a task from request to open PR. Implements, runs the repo's checks, reviews the diff with independent subagents (implementation, then quality, security, design and performance when relevant), fixes blocking findings, opens the PR with `gh` and links a preview. Never merges. Invoke with `/ship`.
- [`better-design`](./better-design/SKILL.md): Design, motion and interaction rules for web (React, Next.js, Tailwind) and React Native / Expo. Loads automatically for frontend work. Run `/better-design audit` for a full audit of existing UI.

## Workflow

1. `/talk` to explore the idea and settle the product decisions.
2. `/ship` to implement it. `ship` uses `better-design` for any UI work and for its design review.
3. Review the PR, test the preview by hand, merge.

## Conventions

- `ship` never merges. It stops at an open PR with a `Problem / Change / Verification / Still Open` body.
- Screenshots of UI changes are attached to the PR (`gh` 2.99+ for `--attach`).
- The preview link uses the Tailscale DNS name when `tailscale` is available, `localhost` otherwise.
- `better-design` values are exact, and every change is expressed in the project's existing styling system.

## Legacy

The previous skill set lives in [`legacy/`](./legacy). It is kept for reference and is no longer maintained:

- [`grill-me`](./legacy/grill-me/SKILL.md): Interview the user about a plan or design until reaching shared understanding.
- [`to-prd`](./legacy/to-prd/SKILL.md): Turn the conversation into a PRD in `docs/prd/`.
- [`to-sub-issues`](./legacy/to-sub-issues/SKILL.md): Split a PRD or ticket into vertical slices in `docs/issues/`.
- [`implement`](./legacy/implement/SKILL.md): Implement `docs/issues` sub-issues with TDD and sequential sub-agents.
- [`frontend`](./legacy/frontend/SKILL.md): Frontend work with bundled design and motion references. Replaced by `better-design`.
- [`diagnose`](./legacy/diagnose/SKILL.md): Diagnosis loop for hard bugs and performance regressions.
- [`refactor-codebase`](./legacy/refactor-codebase/SKILL.md): Find deepening opportunities that make a codebase more testable.

## Attribution

`better-design` condenses MIT-licensed work by Emil Kowalski, Jakub Krehel, Kyle Zantos and Vercel Labs. The legacy skills adapt MIT-licensed work by Matt Pocock and Leonxlnx. See [`NOTICE.md`](./NOTICE.md).

## License

MIT. See [`LICENSE.md`](./LICENSE.md).
