# Global rules

## Language
Code, comments in file, commits, branches and PRs are in English.

In the chat, reply to the user in the language they write in, even when skills and tool output are in English (this rule covers your chat messages, it is never a review finding).

## Git
- Branch names: `<type>/<short-kebab-description>`, e.g. `feat/quote-signature-export`. Types: feat, fix, chore, docs, refactor, perf, test, style, ci, build.
- Never use a tool prefix (`t3code/`, `claude/`, `worktree-agent-*`). If a tool created one, rename it with `git branch -m` before the first commit, without mentioning it.
- Commits: Conventional Commits, a single title line, no body.
- ABSOLUTELY NEVER add `Co-Authored-By:`. ABSOLUTELY NEVER mention Claude or Claude Code in commits or PRs.

## Code
- Write simple, readable code with precise names.
- Split code by responsibility; keep small, related, single-use logic together.
- Reuse existing components and helpers instead of copying them.
- Comments are short (one line if possible) and explain intent, a constraint or a non-obvious decision. Update comments and docs when the code changes.
- Never use EmDash no matter where.

## Errors
- Handle an error only where you can resolve it, translate it or add useful context. Otherwise let the original error propagate.
- Never swallow an error: no empty `catch`, never continue as if the operation succeeded.

## No silent fallbacks
- Never add a fallback, default value, fake data, workaround or degraded mode unless the user asked for it.
- Never return `null`, an empty collection or a fake success to hide a failure.
- You may propose a fallback. Implement it only after approval, and make it explicit, observable, limited and tested.
