---
name: frontend
description: Legacy skill, no longer maintained. Implement frontend/UI work using the bundled design taste and motion design references. Use when user wants a frontend implementation, UI polish, redesign, motion work, or design-heavy interface changes.
---

# Frontend

Implement frontend work only.

Read both reference files before changing UI:

- [frontend-design.md](frontend-design.md)
- [motion-design.md](motion-design.md)

Use the references to guide visual quality, interaction design, motion, states, responsiveness, and implementation details.

## Process

1. Inspect the existing frontend structure, design system, component patterns, styling approach, and available dependencies.
2. Check `package.json` before importing UI, icon, animation, or state libraries.
3. Implement the requested frontend change using existing project conventions where possible.
4. Include expected UI states: loading, empty, error, disabled, hover, active, focus, and responsive behavior when relevant.
5. Verify visually with browser/screenshot when possible.
6. Run the relevant checks for the project.

Do not implement unrelated backend, data model, or product behavior unless it is required to make the frontend change work.
