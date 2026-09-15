# Pattern Library

This file is **vault-wide, not per-project**. It lives once, beside `templates/`, and is never copied into a new project folder by `/crit-ready init`. Every `design-project` instance reads from and writes to this single copy.

It exists to answer the question a project-scoped `design-decisions.md` cannot: *"have we made a call like this before, and what happened?"*

## What goes here

Not every decision graduates here — most stay local to their project. A row belongs in this file only when it is a **reusable trade-off or pattern**, not a one-off fact. Test: would a designer on a *different* product line want to know this before making a similar call? If the answer is specific to this project's constraints only, it stays in that project's `design-decisions.md`.

| Date Promoted | Pattern / Trade-off | Origin Project | Decision Made | Outcome | Tags | Reusable When |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| YYYY-MM-DD | Short name for the recurring situation | project-slug | What was decided | What actually happened after shipping (or "TBD — too early to tell") | comma, separated, tags | The condition under which this precedent applies |

## Rules

- **Never delete a row.** If a pattern turned out to be wrong in a later project, add a new row noting the contradiction and tag both — a broken pattern is still information.
- **Outcome is mandatory before promotion, unless explicitly marked `TBD`.** A decision with no known result is not yet a pattern, just a decision. Promoting untested decisions pollutes the library with things that sound reusable but aren't proven.
- **Tags should describe the situation, not the solution** (e.g. `bulk-action-limits`, `empty-state-ownership`, `permission-edge-case`) so a future project can match on the problem shape, not the specific fix.
- **This file does not replace `design-decisions.md`.** It is a graduation point, not a duplicate. A promoted row should link back to its origin project's decision row (`origin-project/design-decisions.md#row-date`) rather than re-stating the full rationale.

## How rows get here

Only via the `/crit-ready promote` command, run from inside a project's `FOLDER-INSTRUCTIONS.md` context — see Layer 2 there. The agent never promotes automatically; a human decides a decision is reusable, the same way a human decides a decision is confirmed via `/crit-ready sync`.

## How this gets read

`/crit-ready init` on a new project searches this file for tags that overlap with the new project's domain (inferred from its name and the Kickoff answers) and surfaces any matches to the user *before* the Kickoff questions are asked, framed as "here's a precedent from a past project — does it apply here, or is this different?" See `.agents/skills/init-project/SKILL.md`.

Existing projects can also search this file directly any time a decision feels like it might have a precedent — that lookup does not require a special command, just ask the agent to check.
