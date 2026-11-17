# Prep

`/crit-ready prep` prepares the user for one meeting that has not happened yet. It writes the prep into that meeting's own file. After the meeting, `/crit-ready minutes` adds the notes to the same file.

The ideas come from Tom Greever's book *Articulating Design Decisions*. The tactics are listed in `.agents/skills/greever/cheatsheet.md` and `.agents/skills/greever/patterns.md`. Point to those files. Do not copy them out.

Do the steps in order.

## Step 1. Find the project and the rules

1. Find the vault root: the folder that has a `templates/` folder directly inside it.
2. Find the project. A project is a folder with a `FOLDER-INSTRUCTIONS.md` in it.
   - If you are working inside a project folder, use it.
   - Else, if the user named a project, use it.
   - Else, list the projects. If there is one, use it. If there are several, ask "Which project?" and wait.
3. Open the project's `FOLDER-INSTRUCTIONS.md`. Search it for the text `templates/shared/RULES.md`.
   - Found: the project is **current**. Read the file `templates/shared/RULES.md` now. That path starts at the vault root.
   - Not found: the project is **old**. Read the box below.

> **Old project.** Use the project's own `pre-meeting-prep.md` in step 3. The roster is the project's own `stakeholder-mapping.md`. There is no `PRODUCT.md` and no `actions.md`: for open actions, read the unticked `- [ ]` lines in the last meeting file. The Kickoff answers are under "Layer 4" in `FOLDER-INSTRUCTIONS.md`.

## Step 2. Get the meeting details

You need four things: the topic, the date, the meeting type, and who will attend.

- Take them from what the user already said.
- Ask only for the ones that are missing. Ask once, in one message.
- The meeting type is one of: Kickoff, Crit, Executive Review, Handoff, Recurring Sync, Retro. If none fits, pick the closest and say so.

## Step 3. Read the guide for this meeting type

Open `templates/shared/pre-meeting-prep.md`. Each meeting type has a `##` heading (for example the heading that contains `Design Review / Crit`). Find the heading for this meeting type and read from it down to the next `##` heading. That part lists what the prep for this type contains.

## Step 4. Read the project

Read these, in this order. Take notes on what matters for this meeting.

1. `project-brief.md`: the problem and the goal.
2. `FOLDER-INSTRUCTIONS.md`, Kickoff section: the three answers.
3. `meeting-notes.md`: find the last meeting. Open its file.
4. `design-decisions.md`: rows dated on or after the date of the last meeting, and all `Pending` rows.
5. `open-questions.md`: rows in the main table. Do not use rows from the Parked table.
6. `feedback-tracker.md`: rows with Type `✅ Valid` and Status `Open`. Also every row whose "From" is a person attending this meeting.
7. `actions.md`: lines under `## Open`.
8. The product folder's `stakeholder-mapping.md`: the role of each attendee. If an attendee is not in it, take their role from the project's files. Do not edit the roster in this command. In step 8, name the attendees who are missing from it.
9. The product's `PRODUCT.md`: the Standing Decisions table.

To find the product folder: open `FOLDER-INSTRUCTIONS.md`, find the line that starts with `- **Product:**`, follow its link.

## Step 5. Make the meeting file

1. Copy `meetings/_meeting-template.md` to `meetings/YYYY-MM-DD-short-name.md`. Example: `meetings/2026-03-11-checkout-crit.md`. If a file for this meeting already exists, use it and do not make a second one.
2. Fill in the header: Type and Attendees.
3. Add a row to the table in `meeting-notes.md`, directly under the header rows:

   ```
   | 2026-03-11 | Checkout crit | Crit | [meetings/2026-03-11-checkout-crit.md](meetings/2026-03-11-checkout-crit.md) |
   ```

## Step 6. Write the prep

Write under `## Pre-Meeting Prep` in the meeting file. Write in Traditional Chinese (Taiwan).

Which parts to write depends on the meeting type:

| Part | Kickoff | Crit | Executive Review | Handoff | Recurring Sync | Retro |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| A. Opening | yes | yes | yes | yes | no | yes |
| B. What the guide lists for this type | yes | yes | yes | yes | yes | yes |
| C. Predicted reactions | no | yes | yes | no | no | no |
| D. Tactics | no | yes | yes | no | no | no |
| E. Follow-up reminder | yes | yes | yes | yes | yes | yes |

**A. Opening.** Five lines, in this order:

1. The project goal. Take it from the Kickoff answer "What does success look like?" in `FOLDER-INSTRUCTIONS.md`. If that answer is empty or `TBD`, use the Problem section of `project-brief.md` and say the success measure is not set yet.
2. What was agreed last time, in one sentence (from `design-decisions.md` and the last meeting file).
3. What stage the work is at.
4. What feedback the user wants today, and what feedback they do not want.
5. The goal again.

**B. What the guide lists.** Fill each item the guide names for this type, using what you read in step 4. For a Recurring Sync this is a status digest: what changed, what is blocked, which actions are open. It is not a plan to persuade anyone.

**C. Predicted reactions.** One line per attendee who is likely to push back.

- Base each prediction on something that person said before: a row in `feedback-tracker.md` or the Informal Log in `working-notes.md`. Name the row.
- If the project has no record of what a person said before, write "no record for this person yet". Do not guess from their job title.

Example:

```
- Ken (Eng)：可能再提匯出上限的效能問題（見 feedback-tracker 2026-03-04 那一列）。準備：帶上 D-015 的理由。
- Ana (PM)：這個專案還沒有她的回饋紀錄。
```

**D. Tactics.** Pick at most three from the Greever cheatsheet that fit this meeting. For each, say which fact makes it fit. Example: "Rule of Direct Comparison：Ken 上次提出自己的版本，這次並排展示兩個方案。"

**E. Follow-up reminder.** One line: send the written decisions and action items within an hour after the meeting. `/crit-ready minutes` produces them.

If the project has nothing for a field, leave the field empty. Do not fill it with a guess.

## Step 7. Write the changelog line

Add one line at the bottom of the project's `changelog.md`. Copy the format of the lines already there. It says: the date, `prep`, which meeting, which files changed.

## Step 8. Show the user

Show the prep. Name any attendee missing from the roster. Then ask one question: "Do you want to change anything, for example who the swing votes are, or what feedback you want?"

## Check before you finish

- [ ] The meeting file exists and has text under `## Pre-Meeting Prep`.
- [ ] `meeting-notes.md` has a row for this meeting.
- [ ] Every predicted reaction names a row, or says there is no record.
- [ ] `changelog.md` has a new line.
