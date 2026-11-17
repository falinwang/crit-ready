# Minutes

`/crit-ready minutes` takes a transcript (or someone else's summary) and files what it contains into the project hub. The job is finished when the hub is updated, not when a summary has been printed. Notes that stay in chat are lost the next time someone asks "why did we decide that?".

## Steps

1. **Find the project and the rules.** Read the project's `FOLDER-INSTRUCTIONS.md`. If it contains its own File Map, the project predates the shared rules: follow its File Map, its own files and its own table columns, and do not add files to it. Otherwise read `templates/shared/RULES.md` (it also says how to locate the project when the working directory does not make it obvious). A meeting that covers several projects is filed in the project it mostly concerns.

2. **Find the meeting file.** If `/crit-ready prep` already created a file for this meeting in `meetings/`, use it. Otherwise create one from `meetings/_meeting-template.md` as `YYYY-MM-DD-meeting-name.md` and add a row to `meeting-notes.md`. Fill the header (type, attendees, transcript, source type).

3. **Write the notes.** Run `templates/shared/meeting-notes-template.md` (in an old project, the project's own `meeting-notes-template.md`) over the input, in Mode A for a raw transcript or Mode B for second-hand notes, and write the result into the Meeting Notes section of the meeting file.

4. **Route each section** per the File Map. If you are about to write to a section name that is not in the File Map, stop and ask.
   - **Decisions:** check `design-decisions.md` for overlapping rows first, then add new rows with the next IDs. A decision with no stated rationale is added as `Pending`, together with a MEDIUM open question asking for the rationale.
   - **Replacements:** if the meeting explicitly replaces an earlier decision, append the reason to the old row's Rationale and set its status to `Superseded (→ D-NNN)`. If it only looks like a reversal, add the new row and flag it for the user without changing the old row.
   - **Open questions, feedback, informal signals, gaps, exploratory threads, deliverable changes** go to their files per the File Map. Reference Links stay in the meeting file.
   - **Action items** are appended to `actions.md` with a link to the meeting file. In an old project, action items stay as unticked `- [ ]` bullets in the meeting file.
   - **New people** with an identifiable role are added to the product's `stakeholder-mapping.md`.
   - **Standing decisions:** if a new decision conflicts with one in the product's `PRODUCT.md`, flag it to the user. Do not edit `PRODUCT.md`.

5. **Update the changelog.** Append one dated line to the project's `changelog.md` listing what was filed.

6. **Reply to the user** with:
   - A short Slack-ready block: TL;DR, action items, open questions, links to the meeting file.
   - A list of what was written where.
   - What needs the user: attribution cleanup, suspected reversals, `Pending` decisions, Second Brain items that may be worth keeping, and any conflict with a PRODUCT.md standing decision.

## Running it twice

Running this on the same meeting a second time updates the existing rows (same meeting file, same decision, same action item) rather than adding duplicates. Match on the meeting file link and the wording of the row before adding anything.

## Language

Section headers stay in English and the note content is Traditional Chinese (Taiwan), as the notes template says. Do not fill sections with invented content: an empty section is listed on the closing `無內容的段落` line.
