# Pattern Library

This file is **vault-wide, not per-product or per-project**. The live copy sits at the vault root (the folder that contains `templates/`), created once from this schema. It is never copied into a product or project folder. Every project reads from and writes to that single copy.

It exists to answer the question a project's `design-decisions.md` cannot: *"have we made a call like this before, and what happened?"*

## What goes here

Not every decision graduates here. Most stay local to their project. A row belongs in this file only when it is a **reusable trade-off or pattern**, not a one-off fact. Test: would a designer on a *different* product want to know this before making a similar call? If the answer is specific to this project's constraints only, it stays in that project's `design-decisions.md`. If it holds for every project of one product, it belongs in that product's `PRODUCT.md` Standing Decisions instead.

| Date Promoted | Pattern / Trade-off | Origin | Decision Made | Outcome | Tags | Reusable When |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| YYYY-MM-DD | Short name for the recurring situation | `<product>/<project>` D-NNN, linked to the origin row | What was decided | What actually happened after shipping (or "TBD, too early to tell") | comma, separated, tags | The condition under which this precedent applies |

## Rules

- **Never delete a row.** If a pattern turned out to be wrong in a later project, add a new row noting the contradiction and tag both. A broken pattern is still information.
- **Outcome is mandatory before promotion, unless explicitly marked `TBD`.** A decision with no known result is not yet a pattern, just a decision. Promoting untested decisions pollutes the library with things that sound reusable but are not proven.
- **Tags should describe the situation, not the solution** (e.g. `bulk-action-limits`, `empty-state-ownership`, `permission-edge-case`) so a future project can match on the problem shape, not the specific fix.
- **This file does not replace `design-decisions.md`.** It is a graduation point, not a duplicate. A promoted row links back to its origin decision row (`<product>/<project>/design-decisions.md` D-NNN) rather than restating the full rationale.

## How rows get here

Rows arrive only via `/crit-ready promote`. The agent never promotes automatically. A human decides a decision is reusable, the same way a human decides a decision is confirmed via `/crit-ready sync`.

## How this gets read

`/crit-ready init` on a new project searches this file for tags that overlap with the new project's domain (inferred from its name and the Kickoff answers) and surfaces any matches before the Kickoff questions are asked, framed as "here is a precedent from a past project. Does it apply here, or is this different?" See step 9 of `.agents/skills/crit-ready/commands/init.md`.

Any project can also search this file any time a decision feels like it might have a precedent. That lookup does not need a special command, just ask the agent to check.
