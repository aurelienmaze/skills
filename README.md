# Aurelien Maze Skills

This is the set of agent skills I built for my own work, to get the most out of coding agents while keeping control over what they produce. I use them every day to think problems through, ship carefully and hold UI to a high standard. I'm sharing them as-is, so anyone can install or adapt them.

## Install

### 1. Skills

```bash
npx skills@latest add aurelienmaze/skills
```

The picker lists two groups: `Aurelienmaze Skills` (the current set) and `Aurelienmaze Skills Legacy`. To install only the current set:

```bash
npx skills@latest add aurelienmaze/skills --skill talk ship better-design
```

As a Claude Code plugin:

```text
/plugin install aurelienmaze-skills --marketplace aurelienmaze/skills
/plugin install aurelienmaze-skills-legacy --marketplace aurelienmaze/skills
```

### 2. Global rules

[`CLAUDE.md`](./CLAUDE.md) holds the global rules the skills rely on: language, git conventions, code style, error handling and no silent fallbacks. `ship` reviews every diff against them, so install them too. Append them to your global instructions:

```bash
# Claude Code
{ echo; curl -fsSL https://raw.githubusercontent.com/aurelienmaze/skills/main/CLAUDE.md; } >> ~/.claude/CLAUDE.md

# Codex
{ echo; curl -fsSL https://raw.githubusercontent.com/aurelienmaze/skills/main/CLAUDE.md; } >> ~/.codex/AGENTS.md
```

## Skills

- [`talk`](./talk/SKILL.md): Discussion-only mode. Ask questions, compare options or explore an idea while the agent leaves files and project state untouched. Invoke with `/talk`.
- [`ship`](./ship/SKILL.md): Take a task from request to open PR. The agent implements the change, checks it, has it reviewed by independent subagents, then opens the PR with a preview to test. Invoke with `/ship`.
- [`better-design`](./better-design/SKILL.md): Design, motion and interaction rules for the web and React Native. Loads automatically for frontend work, and `/better-design audit` reviews an existing UI.

## Workflow

1. `/talk` to explore the idea and settle the product decisions.
2. `/ship` to implement it. `ship` uses `better-design` for any UI work and for its design review.
3. Review the PR, test the preview by hand, merge.

## Legacy

The previous skill set lives in [`legacy/`](./legacy). It is kept for reference and is no longer maintained. These skills are still installable, grouped under `Aurelienmaze Skills Legacy`, and each description starts with `Legacy skill, no longer maintained.`:

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
