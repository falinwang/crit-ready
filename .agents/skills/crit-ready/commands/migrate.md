# Migrate

`/crit-ready migrate [project]` converts one older project to the current structure: shared rules instead of a private copy, decision IDs, a single `actions.md`, and a product it belongs to. It changes a project's real history files, so it runs only when the user asks, one project at a time, and nothing is changed before the user has seen the plan.

An older project is one whose `FOLDER-INSTRUCTIONS.md` contains its own File Map. If the project already points to `templates/shared/RULES.md`, say it is already current and stop.

## 1. Check the vault first

The current structure needs the current templates. Look for `templates/shared/RULES.md` and `templates/product/` at the vault root (the folder that contains `templates/`). If they are missing, the vault still has the older templates: tell the user to update the vault's `templates/` and skills from the Crit-Ready repository first, and stop. Do not write the shared files from memory.

Then read `templates/shared/RULES.md`.

## 2. Read the project and write the plan

Read every file in the project folder. Then show the user a plan that lists, per file, what will change and what you could not decide. Include:

- Which product this project belongs to, and where that product's folder will be (see step 4).
- How many decision rows get IDs, and any `Superseded (→ date)` that cannot be resolved to one row.
- How many action items were found in meeting files, open and done.
- Which people move to the product roster, and any who conflict with a row already there.
- Whether the project's own `meeting-notes-template.md` or `pre-meeting-prep.md` differs from the shared version, and how.
- Any file in the folder that is not part of Crit-Ready. These are left alone.

Wait for the user to approve the plan. Their answers to the open points go into the plan before anything is written.

## 3. Back up

Before the first change, make a full copy of the project folder as `<project>.pre-migration-YYYY-MM-DD` beside it, or wherever the user prefers. If the vault is a git repository with no uncommitted changes in the project, a commit is enough of a restore point and the copy can be skipped; say which one you relied on. Tell the user where the backup is and that they can delete it once they are satisfied.

## 4. Resolve the product

Ask the user which product this project belongs to if it is not obvious. Follow the layout rules in `RULES.md`: the vault's own conventions decide where the product folder sits, and the project folder itself does not move unless the user asks for that.

- If the product already has a Crit-Ready `PRODUCT.md`, use it.
- Otherwise create the product folder from `templates/product/` and fill in the name and description from the project's `project-brief.md`.

Add the project to the Projects table in `PRODUCT.md`.

## 5. Convert the files

Work through the files in this order. Keep every existing row and its wording. Add columns and IDs; do not rewrite content.

1. **`FOLDER-INSTRUCTIONS.md`.** Replace it with the current template. Carry over the three Kickoff answers exactly as written. Compare the old file with the stock text of its time: anything the user added or changed for this project goes under Project-specific instructions, word for word. When unsure whether a passage is stock or custom, keep it there.
2. **`design-decisions.md`.** Add the `ID` column and number the rows `D-001` onward in their existing order. Rewrite each `Superseded (→ date)` to point at the ID of the row that replaced it. If two rows share that date and the replacement is not clear from the Rationale, ask instead of choosing. Update the header notes to the current template's.
3. **`open-questions.md`.** Add the `Urgency` and `Blocks` columns. Fill them only where the project's meeting notes or the row itself state them; otherwise leave them blank for the user. Move resolved rows into a `Closed` section, keeping their struck-through text and resolution. Where a resolution names a decision by date, add its new ID.
4. **`actions.md`.** Create it from the template. Collect every action item from the Action Items sections of the meeting files: unticked ones go under Open, ticked ones under Done, each with a link to its meeting file. Leave the checkboxes in each meeting's Attribution Cleanup section where they are, since those are not action items.
5. **Meeting files.** Past meeting files are records. Change only two things: turn the Action Items checkboxes into plain bullets (the live checkbox is now in `actions.md`), and leave everything else as it was written.
6. **`stakeholder-mapping.md`.** Merge its rows into the product's roster. Treat the same person under two spellings as one row. If a person already in the roster has a different team or function, show both and ask. Notes about who has final approval for this project move to the Roles table of `project-brief.md`. Then remove the project's copy, which now lives in the backup.
7. **`meeting-notes-template.md` and `pre-meeting-prep.md`.** These are now shared. If the project's copy carries nothing the shared version lacks, remove it. If the user customised it, show the differences and ask whether to keep them as Project-specific instructions in `FOLDER-INSTRUCTIONS.md` before removing the copy.
8. **Cross-references.** Where other files in the project point at a decision by date (`feedback-tracker.md`, `deliverables.md`, `working-notes.md`), add the ID beside the date when the match is unambiguous.
9. **`changelog.md`.** Append one dated line saying the project was migrated and where the backup is.

Leave alone: `project-brief.md` apart from the Roles note above, `feedback-tracker.md`, `working-notes.md`, `deliverables.md`, `meeting-notes.md`, and any file that is not part of Crit-Ready.

## 6. The pattern library

Migration does not move the pattern library. If the vault keeps a live one at `templates/pattern-library.md`, it stays there and the other commands keep using it. Rows already promoted from this project still link to its `design-decisions.md`; add the decision ID to those rows if the match is unambiguous.

## 7. Report

Tell the user:

- What was changed, file by file, with counts (decisions numbered, actions collected, people merged).
- What was left for them: blank Urgency or Blocks fields, ambiguous supersede links, roster conflicts.
- Where the backup is.
- That the project now follows the shared rules, so the other commands treat it as a current project from the next run.

Nothing in this command deletes history. If a step would lose information that is not in the backup, stop and ask.
