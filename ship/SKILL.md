---
name: ship
description: Implement a task, review it with independent subagents, then open a PR and a preview. Use ONLY when the user invokes /ship.
disable-model-invocation: true
---

# Ship

Take a task from request to open PR. Never merge.

## 1. Input
Use the brief or spec file if there is one and use the user's message in any case.
If a product decision is ambiguous, ask before coding.

## 2. Implement
- Use the /better-design skill for any UI work.
- Run the repo's checks (typecheck, lint, tests, build) and fix what fails.
- If the change has UI and a browser tool is available, start the app on a free port, check the changed screens at desktop and mobile width, and save screenshots. Keep the server running.

## 3. Review
Spawn independent subagents with a fresh context. Give them the brief. Each returns findings, blocking ones first, no style nitpicks.
1. Implementation: does the change do what the brief asks, with nothing missing ?
2. Then, in parallel:
   - Quality: AGENTS.md or CLAUDE.md global rules, duplication, naming, error handling.
   - Security: only if the diff touches auth, user input, data access, secrets or external calls. Skip it otherwise.
   - Design: only if the diff touches UI. Run the better-design light pass on the diff. Skip it otherwise.
   - Performance: only if the diff touches data fetching, server rendering, database queries or schema, or adds client-side dependencies. Keep it short. Skip it otherwise.

## 4. Fix
Fix blocking findings and rerun the checks. Rerun a reviewer if the fix is non-trivial. Stop after a max of 2 turns and list what is still open.

## 5. Ship
- Commit and push the branch.
- Open the PR with `gh pr create`, using exactly this body:

  ```
  ## Problem
  ## Change
  ## Verification
  ## Still Open (only if there are open findings)
  ```

  Change: what changed, plus screenshots if the change has UI. Verification: a short list of what was checked.
- Screenshots: write the body to a file, reference each one under Change as `![alt](/abs/path/shot.png)`, and pass the same path with `--attach` (gh 2.99+).

## 6. Preview
If `tailscale` is available, link `http://<Self.DNSName from tailscale status --json>:<port>`. Otherwise link `http://localhost:<port>`.

End with the PR link, the preview link, screenshots, and what the user should test by hand.