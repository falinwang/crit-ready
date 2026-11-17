# Minutes

`/crit-ready minutes` takes a meeting transcript, or someone's notes about a meeting, and files it into the project.

You are finished only when the project files are updated. Printing a summary in chat is not finishing.

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

> **Old project.** Use the File Map inside the project's own `FOLDER-INSTRUCTIONS.md`. Use the project's own `meeting-notes-template.md`. Its tables have no ID column: do not add IDs, and mark a replaced decision `Superseded (→ YYYY-MM-DD)`. Keep action items in the meeting file as `- [ ]` lines. Do not create `actions.md`. The roster is the project's own `stakeholder-mapping.md`. Skip step 7.

## Step 2. Decide the input type

Look at what the user gave you.

- It is word-for-word speech (a transcript, with or without speaker names): this is **Mode A**.
- It is a summary someone or some tool already wrote: this is **Mode B**.
- You cannot tell: treat it as **Mode B**.

In Mode B, never add a speaker name, a decision or a detail that the summary does not contain.

## Step 3. Find or make the meeting file

1. Find out the meeting's date and name from the input. If the date is not in the input, ask the user.
2. Look in the project's `meetings/` folder for a file for this meeting (same date, same meeting). `/crit-ready prep` may have made it already.
3. If it exists, use it. Keep its Pre-Meeting Prep section as it is.
4. If it does not exist:
   1. Copy `meetings/_meeting-template.md` to `meetings/YYYY-MM-DD-short-name.md`. Example: `meetings/2026-03-04-design-crit.md`.
   2. Add a row to the table in `meeting-notes.md`, directly under the header rows, so the newest meeting is first:

      ```
      | 2026-03-04 | Design crit | Crit | [meetings/2026-03-04-design-crit.md](meetings/2026-03-04-design-crit.md) |
      ```
5. Fill in the header of the meeting file: Type, Attendees, Transcript, Source type (`Raw transcript` for Mode A, `Pre-digested notes` for Mode B).
   - Type is one of: Kickoff, Crit, Executive Review, Handoff, Recurring Sync, Retro. If the input does not say, pick the closest one from the meeting's name and content and write `(inferred)` after it. Example: a meeting named "Design System Sync" is `Recurring Sync (inferred)`.
   - Attendees are the people who were in the meeting. People who were only mentioned are not attendees.

## Step 4. Write the notes

1. Open `templates/shared/meeting-notes-template.md`. Read all of it.
2. Write every section it lists, in its order, using its formats. Put the result under `## Meeting Notes` in the meeting file. Section headings inside the notes use `###`, as in the template.
   - If the input is already written in the template's sections, keep its wording. Add only what the template asks for and the input lacks (for example the decider on each decision). Do not rephrase what is there.
3. Section headers stay in English. The content is Traditional Chinese (Taiwan).
4. If a section has nothing to say, leave it out. At the very end of the notes add one line that names the sections you left out:

   ```
   無內容的段落：Known Gaps Acknowledged、Still Exploratory
   ```
5. Do not invent content to fill a section.
6. In the meeting file, write action items as plain bullets with no checkbox:

   ```
   - 更新付款頁的錯誤文案 | 負責人：Mei (Design) | 期限：2026-03-08
   ```

## Step 5. File each section

Go through this table row by row. For each section that has content, write it to the file named. Use the columns that the file's header row already has.

| Section in the notes | Write to | How |
| :--- | :--- | :--- |
| Design Decisions & Articulation | `design-decisions.md` | See step 6 |
| Outcomes: ✅ 通過 | `design-decisions.md` | Only if it is not already written as a decision. See step 6 |
| Outcomes: ⏸ 延後, ⚖️ 取捨 | `working-notes.md`, table "Deferred & Trade-offs" | One row each |
| Open Questions | `open-questions.md` | One row each. Status `Open`. Example below |
| Feedback Log | `feedback-tracker.md` | One row each. Status `Open`, or `Closed` if it was settled in the meeting |
| Informal Signals Captured | `working-notes.md`, table "Informal Log" | One row each. Copy the words as spoken. In the Formalise? column write `Yes` for 是, `No` for 否, `Watching` for 持續觀察 |
| Known Gaps Acknowledged | `working-notes.md`, list "Known Gaps" | One bullet each, ending with the date. Add who raised it only if the notes name the person |
| Still Exploratory | `working-notes.md`, list "Still Exploratory" | One bullet each |
| Deliverable Status Changes | `deliverables.md` | If the deliverable has a row, update it. If not, add a row |
| Problem & Goal | `project-brief.md` | Change the brief only if the notes say in words that the goal or the scope changed. If they do not say that, do not edit the brief: in step 9, tell the user what the meeting said about the goal |
| Action Items | `actions.md`, under `## Open` | One checkbox line each. Example below |
| Stakeholder Register | The Attendees line of the meeting file | Also: a new person whose team or function is known gets a row in the product folder's `stakeholder-mapping.md`. Fill what is known and leave the rest empty. A person with neither known is not added: name them in step 9 |
| TL;DR, Reference Links, Hub Routing, Second Brain Prompt, Attribution Cleanup | Stay in the meeting file | Do nothing more |

Example row for `open-questions.md`:

```
| 2026-03-04 | 2026-03-04 | 匯出上限要設在幾筆？ | HIGH | 匯出功能的規格無法定案 | Ken (Eng) | Open |
```

Example line for `actions.md` (it has a checkbox and a link to the meeting file):

```
- [ ] 更新付款頁的錯誤文案 | 負責人：Mei (Design) | 期限：2026-03-08 | 來源：[2026-03-04 Design crit](meetings/2026-03-04-design-crit.md)
```

If the notes contain a section that is not in this table and not in the File Map: stop and ask the user where it goes.

## Step 6. File the decisions

Do this for each decision, one at a time.

1. Search `design-decisions.md` for a row about the same topic.
2. Choose one case:

   | Case | What to do |
   | :--- | :--- |
   | No row is about this topic | Add a new row at the bottom of the table |
   | A row already says the same thing | Do not add a row. Update that row if there is something new |
   | The meeting said clearly that this replaces an older decision | Add the new row. Then in the old row: add `Replaced by D-NNN:` and the new decision's reason to the end of Rationale, and set Status to `Superseded (→ D-NNN)` using the new row's ID |
   | It seems to contradict an older row, but the meeting did not say it replaces it | Add the new row with Status `Pending`. Do not change the old row. Tell the user in step 9 |

3. The new row's ID is the highest ID in the table plus 1.
4. Choose the Status:
   - `Active`: the notes present it as decided and give the reason. If the notes do not name who decided, it is still `Active`: write `拍板：待確認` in Source / Owner.
   - `Pending`: the reason is missing, or it was a casual remark, or the notes say it still waits for someone's answer or approval. Say in Rationale what is missing.
   - `Blocked`: agreed, but waiting on something outside the team. Name it in Rationale.
5. If the Status is `Pending` because the reason is missing, also add a row to `open-questions.md` asking for the reason, with Urgency `MEDIUM`.

Example row:

```
| D-015 | 2026-03-04 | 匯出一次最多 500 筆 | 超過 500 筆時頁面會逾時，客服回報過三次 | [2026-03-04 Design crit](meetings/2026-03-04-design-crit.md), 拍板：Ken (Eng) | Active | bulk-action-limits |
```

Never delete a row.

## Step 7. Check the product's standing decisions

1. Open the project's `FOLDER-INSTRUCTIONS.md`. Follow the link on the `- **Product:**` line to `PRODUCT.md`.
2. Read its Standing Decisions table.
3. If a decision from this meeting disagrees with a row there, remember it for step 9. Do not edit `PRODUCT.md`.

## Step 8. Write the changelog line

Add one line at the bottom of the project's `changelog.md`. Copy the format of the lines already there. It says: the date, `minutes`, what you added, which files you changed. Count the rows you really wrote before you write the numbers.

## Step 9. Reply to the user

Reply with these three parts, in this order.

**Part 1: a short summary the user can paste into Slack.** TL;DR, the action items, the open questions, and the path of the meeting file. Write it in the language of the notes.

**Part 2: what you wrote and where.** One line per file. Example: `design-decisions.md: added D-015, D-016; D-009 marked Superseded`.

**Part 3: what the user has to do.** List only the ones that apply:

- Speakers you could not identify (Attribution Cleanup).
- Decisions that seem to contradict an older one.
- Decisions you filed as `Pending`, and what is missing for each.
- Items in the Second Brain Prompt section.
- People you did not add to the roster because their team and function are unknown.
- What the meeting said about the goal, if you did not change `project-brief.md`.
- Conflicts with a standing decision in `PRODUCT.md`.

## If this meeting was already filed

If the meeting file already has notes, you are running a second time. Update the rows you wrote before. Do not add them again. Before adding any row, check whether a row with the same meeting link and the same content is already there.

## Check before you finish

- [ ] The meeting file exists and has the notes under `## Meeting Notes`.
- [ ] `meeting-notes.md` has a row for this meeting.
- [ ] Every decision is in `design-decisions.md` with an ID.
- [ ] Every action item is in `actions.md` with a checkbox and a link.
- [ ] `changelog.md` has a new line.
- [ ] Nothing was invented, and no row was deleted.
