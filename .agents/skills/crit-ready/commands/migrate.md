# Migrate

`/crit-ready migrate [project]` converts one old-format project to the current format.

This command changes a project's real history files. So:

- Run it only when the user asks for it.
- Convert one project at a time.
- Change nothing until the user has seen the plan and said yes.
- Keep every existing row and its words. Add columns and IDs. Do not rewrite content.

Do the steps in order.

## Step 1. Check the vault

1. Find the vault root: the folder that has a `templates/` folder directly inside it.
2. Check that these exist: `templates/shared/RULES.md` and the folder `templates/product/`.
   - Both exist: read `templates/shared/RULES.md` and go to step 2.
   - One is missing: the vault still has the old templates. Say "Update the vault's `templates/` folder and the crit-ready skill from the Crit-Ready repository first." Then stop. Do not write those files from memory.

## Step 2. Check that the project is old

Open the project's `FOLDER-INSTRUCTIONS.md`. Search it for the text `templates/shared/RULES.md`.

- Found: the project is already current. Say so and stop.
- Not found: the project is old. Go to step 3.

## Step 3. Read the project and write the plan

Read every file in the project folder. Then write a plan for the user. The plan lists:

1. The product this project will belong to, and where the product folder will be (see step 5).
2. How many decision rows will get IDs.
3. Every `Superseded (→ date)` where two or more rows have that date. For each, write which row you think replaced it and why (for example: same tags, same topic). The user confirms or corrects this when they approve the plan.
4. How many action items you found in the meeting files: how many open, how many done.
5. Which people will move to the product roster, and any who are already there with a different team or function.
6. Whether the project's `meeting-notes-template.md` and `pre-meeting-prep.md` are the same as the standard ones. If they differ, show how.
7. Anything in `FOLDER-INSTRUCTIONS.md` that the user added, such as extra rows in the File Map.
8. An agent instruction file in the project (`AGENTS.md`, `CLAUDE.md`) that describes the old format.
9. Any other to-do list in the project (for example `NEXT.md`). Ask: "Leave it as it is, or move its open items into `actions.md`?"
10. Files that are not part of Crit-Ready. These will not be touched.

Show the plan. Ask the user to answer the open points and to approve. Wait. Do not go to step 4 before the user says yes.

## Step 4. Make a backup

1. Copy the whole project folder to a folder **outside the vault root**, named `<project>-pre-migration-YYYY-MM-DD`. Use another place only if the user names one.
2. Do not put the backup inside the vault. A copy inside the vault still has a `FOLDER-INSTRUCTIONS.md`, so `/crit-ready today` would treat it as a second project.
3. Compare the copy with the original to make sure it is complete.
4. Tell the user where the backup is.

If the vault is a git repository and the project has no uncommitted changes, the last commit is the backup and you can skip the copy. Say which one you relied on.

## Step 5. Find or create the product

1. Ask the user which product this project belongs to, unless it is obvious.
2. Decide where the product folder goes: follow the vault's own conventions (its `AGENTS.md`, `CLAUDE.md` or `README.md`). If there are none, put the product folder in the vault root. The project folder itself stays where it is, unless the user asks to move it. In that case the product folder does not contain the project, and that is fine: the Product link connects them.
3. If the product already has a `PRODUCT.md` with a "Projects" table and a "Standing Decisions" table, use it.
4. If not, create the product folder and copy the two files from `templates/product/` into it. Fill in the product name. Fill in the description only from what the project's files say.
5. Add this project as a row in the Projects table of `PRODUCT.md`.

## Step 6. Convert the files

Do these in order, one file at a time.

**6.1 `design-decisions.md`**

1. Add a first column named `ID` to the decisions table.
2. Number the rows from top to bottom: `D-001`, `D-002`, `D-003`, and so on.
3. Change each `Superseded (→ date)` to `Superseded (→ D-NNN)`, using the ID of the row that replaced it. If you cannot tell which row that is, use the user's answer from the plan.
4. In the notes below the table, change `Superseded (→ YYYY-MM-DD)` to `Superseded (→ D-NNN)`.

Before and after:

```
| 2026-03-04 | 匯出一次最多 500 筆 | ... |
| D-001 | 2026-03-04 | 匯出一次最多 500 筆 | ... |
```

**6.2 `open-questions.md`**

1. Add two columns after Question: `Urgency` and `Blocks`.
2. Fill them only when the row itself or the meeting notes state them. If a row's question text ends with words like "Medium urgency. Affects the handoff.", move those words into the two columns. Otherwise leave the two cells empty.
3. Add a `## Closed` section. Move resolved rows into it. Keep their struck-through text and their resolution.

**6.3 `actions.md`** (new file)

1. Copy `templates/design-project/actions.md` into the project.
2. Open each meeting file. Find the section whose heading contains `Action Items`.
3. Each `- [ ]` line there goes under `## Open`. Each `- [x]` line goes under `## Done`, still starting with `- [x]`, and ending with ` | 完成：日期未記錄` unless the file says when it was done. In `actions.md` every line keeps its checkbox; only the meeting file loses it (step 6.4).
4. Add ` | 來源：[meeting name](meetings/file-name.md)` to the end of each line.
5. Checkboxes in other sections (for example Attribution Cleanup) are not action items. Leave them.

**6.4 Meeting files**

Change one thing only: in the Action Items section, turn `- [ ] ` and `- [x] ` into `- `. Leave every other line exactly as it is. Then replace `meetings/_meeting-template.md` with the current one from `templates/design-project/meetings/`.

**6.5 The roster**

1. Copy each person row from the project's `stakeholder-mapping.md` into the product folder's `stakeholder-mapping.md`.
2. The same person under two spellings is one row.
3. If a person is already in the product roster with a different team or function, use the user's answer from the plan.
4. Links in the copied rows pointed at files in the project. Rewrite them so they work from the product folder.
5. A note about who has final approval for this project goes under the Roles table in the project's `project-brief.md`.
6. Delete the project's `stakeholder-mapping.md`. A copy is already in the backup.

**6.6 The project's own copies of shared files**

For `meeting-notes-template.md` and `pre-meeting-prep.md` in the project folder:

- Same as the standard version: delete it from the project. A copy is already in the backup.
- Changed by the user: do what the user chose in the plan. Either keep the changes as text under "Project-specific instructions" in `FOLDER-INSTRUCTIONS.md`, or drop them. Then delete the file from the project.

**6.7 `FOLDER-INSTRUCTIONS.md`**

1. Save the three Kickoff answers from the old file, word for word.
2. Save anything the user added to the old file (item 7 of the plan), word for word. The numbered layers (`Layer 1` to `Layer 5`), the standard File Map rows and the standard notes under them are template text, not user additions: they are replaced by `RULES.md`. The user's additions are things like extra File Map rows, navigation links, or project-specific notes.
3. Replace the file with `templates/design-project/FOLDER-INSTRUCTIONS.md`.
4. Fill the four lines under `## Project`. Name: the project's name from its `project-brief.md`, or else its folder name. Follows: `none` unless the user says otherwise. Status: `Active`, unless the user says the project is paused or finished. The Product link must lead to the product's `PRODUCT.md`.
5. Put the three Kickoff answers in the `## Kickoff` section.
6. Put what the user added under `## Project-specific instructions`. Extra File Map rows go in a small table there. Fix links that now point at moved files.

**6.8 Small fixes**

- In `meeting-notes.md`, the text above the table may mention a numbered layer of the old `FOLDER-INSTRUCTIONS.md`. Change that mention to point to `templates/shared/RULES.md`. Do not change the rows.
- Where `feedback-tracker.md`, `deliverables.md` or `working-notes.md` refers to a decision by its date, add the ID next to the date, but only if exactly one decision has that date.

**6.9 Things the user decided in the plan**

- Agent instruction file (`AGENTS.md`, `CLAUDE.md`): if the user approved, change only the sentences that are now wrong (layer numbers, where action items live, where the roster is, old skill names). Leave the rest.
- Other to-do list: if the user chose to move it, add its open items to `actions.md`, skipping any that repeat an action item you already collected. Leave one line in the old file that points to `actions.md`. Keep its frontmatter.

**6.10 `changelog.md`**

Add one line at the bottom, in the format the file already uses. It says: the date, that the project was migrated, what changed, and where the backup is.

## Step 7. Check your work

1. Compare the project with the backup. The only files that differ must be the ones in step 6.
2. In each meeting file, the only changed lines must be the action item lines.
3. Check every link in the project and in the product folder. Fix any that do not resolve.

## Step 8. The pattern library

Do not move the pattern library. If it is at `templates/pattern-library.md`, it stays there.

## Step 9. Reply to the user

Tell the user:

1. What changed, file by file, with numbers (decisions numbered, actions collected, people moved).
2. What is left for them: empty Urgency or Blocks cells, actions with no owner, actions that look finished but are not ticked.
3. Where the backup is.
4. That the other commands now treat this project as current.

## Stop and ask the user when

- A `Superseded (→ date)` could point at more than one row.
- A person is in two rosters with different roles.
- You cannot tell whether a passage in the old `FOLDER-INSTRUCTIONS.md` is standard text or something the user wrote. In that case keep it.
- A step would lose information that is not in the backup.

## Check before you finish

- [ ] The user approved the plan before any change.
- [ ] The backup is outside the vault and complete.
- [ ] No row and no meeting text was deleted or reworded.
- [ ] `FOLDER-INSTRUCTIONS.md` contains the text `templates/shared/RULES.md`.
- [ ] Every link resolves.
- [ ] `changelog.md` has a new line.
