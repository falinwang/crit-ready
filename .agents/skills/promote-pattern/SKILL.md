---
name: promote-pattern
description: "Use this skill to graduate a project decision to a product standing decision or to the vault-wide pattern library. Trigger this when the user says /crit-ready promote."
---

# Promote

Promotion is human-triggered only. Never promote a decision on your own initiative, and never because a decision "looks reusable". The user decides that.

There are two targets.

- `/crit-ready promote [decision] to product` adds a Standing Decision to the product's `PRODUCT.md`: a decision that stays in force across the product's projects.
- `/crit-ready promote [decision]. Outcome: [...]. Tags: [...]` adds a row to the vault-wide `pattern-library.md`: a precedent a designer on a different product might want.

## First

Find the project and the rules. Read the project's `FOLDER-INSTRUCTIONS.md`. If it contains its own File Map, the project predates the shared rules: use its own table columns and do not add files to it. Otherwise read `templates/shared/RULES.md`, which also says how to locate the project. Then find the decision row in the project's `design-decisions.md`. If it is ambiguous which row the user means, ask.

## Promote to product

1. Open the product's `PRODUCT.md` (the one in the parent folder of the project). If there is none, tell the user and stop. Do not create one here, `/crit-ready init` does that.
2. Add a row to Standing Decisions with the next `PD-NNN`, the decision, a link back to the origin row (`<project>/design-decisions.md` D-NNN), today's date and status `Active`. No Outcome is needed. Do not restate the rationale, link to it.
3. If a standing decision already says the same thing or conflicts with this one, show it to the user before adding. A replacement marks the old row `Superseded (→ PD-NNN)`. Never delete a row.

## Promote to the pattern library

1. **Check the Outcome.** Refuse if there is no known outcome, unless the user explicitly marked it `TBD`. An untested decision is not yet a pattern.
2. **Locate the library.** It lives at the vault root, the folder that contains `templates/`. If an older setup has a live one at `templates/pattern-library.md`, use that one and never create a second. If none exists, create `pattern-library.md` at the vault root from `templates/vault/pattern-library.md`.
3. **Add a row** with today's date, a short name for the situation, the origin as `<product>/<project>` with the decision ID and a link to the origin row, the decision, the Outcome, the tags (describing the situation, not the fix) and when the precedent applies. Do not restate the full rationale: link to it.
4. Never delete a row. If a later project contradicts a pattern, add a new row noting the contradiction.

## Afterwards

Append one dated line to the project's `changelog.md`, then confirm to the user what was added and where.
