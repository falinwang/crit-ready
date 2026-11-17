# Sync Design Decision

Typical invocation: `/crit-ready sync [Decision] by [Who/Source]. [Reason]. [Replaces]`. The decision text may also be missing, in which case use the source from the current conversation (see "No decision text given").

## Before editing

1. **Find the project and the rules.** Read the project's `FOLDER-INSTRUCTIONS.md`. If it contains its own File Map, the project predates the shared rules: follow its File Map, its own files and its own table columns (dates instead of IDs), and do not add files to it. Otherwise read `templates/shared/RULES.md`, which also says how to locate the project.
2. Read the header, Status Values and Rules sections of `design-decisions.md`. Use the table's actual columns. Do not assume them.
3. Figma comments and Slack are tier 4 sources. `/crit-ready sync` is what formalizes them, so cite the platform, the person and the date in Source / Owner. If the source names a decider, record that name too.

## No decision text given

Look for a source earlier in this conversation (Figma comments, Slack thread, pasted text) and extract only decisions that were actually concluded: a resolved thread, an explicit confirmation from the owner, or an agreement between named people.

- Do not log open questions, suggestions or reviewer asks as decisions. List them to the user as unlogged instead.
- If nothing in the conversation qualifies, ask the user what to sync. Do not invent one.

## Steps

1. **Search and supersede.** Search `design-decisions.md` for overlapping rows (grep on key terms). If the new decision explicitly replaces or obviously conflicts with an old one, append the reason for the change to the old row's Rationale, then set its Status to `Superseded (→ D-NNN)` pointing to the new row's ID. In an old project without an ID column, point to the new row's date instead. If a matching row already exists, update it rather than adding a duplicate. Never delete a row.
2. **Record.** Append the new row after the last table row, with the next ID (if the table has an ID column), today's date, the source, the rationale and tags (tags describe the shape of the problem; reuse existing tags where they fit). Choose Status by the hub's own rules:
   - `Active`: confirmed by a verifiable source and owned by someone (the owner, Product, or the people the thread agreed on).
   - `Pending`: one person's proposal, a casual remark, or no explicit sign-off from the owner. Say in Rationale what confirmation is missing.
   - `Blocked`: agreed in principle but held by an external condition, named in Rationale.
3. **Clear.** Check `open-questions.md`. If this sync resolves an open question, move the row to the Closed section with the question struck through, the resolution (cite the decision ID) and today's date. If it only partly answers one, add a dated update to that row and leave it open. Keep that file's own language and row format.
4. **Follow-up tasks.** If the source implies a task (for example "Eng to confirm the limit"), add it to `actions.md` with a link to the decision row. In an old project, mention it to the user instead of adding a file.
5. **Standing decisions.** If the new decision contradicts a standing decision in the product's `PRODUCT.md`, flag it to the user. Do not edit `PRODUCT.md`.
6. **Changelog.** Append one dated line to the project's `changelog.md`.
7. **Report.** Tell the user what was added, superseded and closed, and list anything seen in the source but deliberately not logged (open questions, unresolved asks) with why.
8. **Lock-in phrase.** Output one sentence the user can paste into Slack or Figma to lock in agreement with the stakeholder (for example "Got it, I've recorded that..."). If any logged row is `Pending`, the phrase should ask the stakeholder to confirm it.
