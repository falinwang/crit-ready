# Sync

`/crit-ready sync` records a decision that was made outside a meeting: in Slack, in a Figma comment, in a chat thread.

The usual form is:

```
/crit-ready sync [Decision] by [Who/Source]. [Reason]. [Replaces]
```

Example:

```
/crit-ready sync Export is capped at 500 rows by Ken in Slack #design. Larger exports time out. Replaces the 1000-row cap.
```

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

> **Old project.** Its tables have no ID column: do not add IDs. Mark a replaced decision `Superseded (→ YYYY-MM-DD)` with the date of the new row. Do not create `actions.md`: tell the user about follow-up tasks instead. Skip step 7.

4. Open `design-decisions.md`. Read its header row, its Status Values table and its Rules. Use the columns the table really has.

## Step 2. Find the decision

**If the user typed the decision:** use it. Go to step 3.

**If the user typed `/crit-ready sync` with nothing after it:** look earlier in this conversation for a Slack thread, Figma comments or pasted text.

- Take only what was really decided. A decision is one of these: a thread marked resolved, a clear "yes, do that" from the person who owns the work, or an agreement between named people.
- A question is not a decision. A suggestion is not a decision. A request from a reviewer is not a decision. Do not record these. List them for the user in step 9 as "not recorded".
- If you find no decision, ask the user "What should I record?" and stop. Do not invent one.

## Step 3. Look for an older row about the same thing

Search `design-decisions.md` for rows about the same topic. Search for the main words of the decision.

Choose one case:

| Case | What to do |
| :--- | :--- |
| No row is about this topic | Go to step 4 |
| A row already says the same thing | Update that row (for example, add the new source). Do not add a new row. Skip step 4 |
| The new decision replaces or contradicts an older row | Do step 4 first. Then come back and change the old row: add `Replaced by D-NNN:` and the new decision's reason to the end of its Rationale, and set its Status to `Superseded (→ D-NNN)` using the new row's ID |

Never delete a row.

## Step 4. Add the new row

Add one row at the bottom of the decisions table.

- **ID**: the highest ID in the table plus 1.
- **Date**: today.
- **Decision**: what was decided.
- **Rationale**: the reason given. If no reason was given, write that the reason is missing.
- **Source / Owner**: the platform, the person, and the date. Slack and Figma comments are the weakest kind of source, so always say exactly where it came from. If the source names who made the final call, add that name.
- **Tags**: words for the kind of problem, not for the fix. Reuse tags already in the table when they fit.
- **Status**: choose one.

  | Status | Use it when |
  | :--- | :--- |
  | `Active` | A source you can point to confirms it, and someone owns it. A Slack message or Figma comment is enough when the person who owns that area states the decision plainly |
  | `Pending` | One person proposed it, or it was a casual remark, or the owner has not said yes. Write in Rationale what confirmation is missing |
  | `Blocked` | It is agreed, but waiting on something outside the team. Name that thing in Rationale |

Example row:

```
| D-016 | 2026-03-05 | 匯出一次最多 500 筆 | 超過 500 筆會逾時 | Slack #design, Ken (Eng), 2026-03-05 | Active | bulk-action-limits |
```

## Step 5. Close open questions it answers

Open `open-questions.md`.

- If the decision fully answers a question: move that row to the `Closed` section. Strike through the question text with `~~`, write the resolution with the decision ID, and write today's date. If the file has no Closed section, add one.
- If the decision answers only part of a question: add a dated note to that row and leave it open.
- Keep the language and the row format the file already uses.

Example closed row:

```
| 2026-03-04 | 2026-03-05 | ~~匯出上限要設在幾筆？~~ | 500 筆，見 D-016 |
```

## Step 6. Record follow-up tasks

If the source says someone has to do something (for example "Eng will confirm the limit"), add a line under `## Open` in `actions.md`:

```
- [ ] 確認匯出上限對效能的影響 | 負責人：Ken (Eng) | 期限：TBD | 來源：D-016
```

## Step 7. Check the product's standing decisions

1. Open the project's `FOLDER-INSTRUCTIONS.md`. Follow the link on the `- **Product:**` line to `PRODUCT.md`.
2. If the new decision disagrees with a row in its Standing Decisions table, remember it for step 9. Do not edit `PRODUCT.md`.

## Step 8. Write the changelog line

Add one line at the bottom of the project's `changelog.md`. Copy the format of the lines already there. It says: the date, `sync`, what changed, which files changed.

## Step 9. Reply to the user

Reply with these parts.

1. **Added**: the new row's ID and text.
2. **Superseded**: any old row you marked, and why.
3. **Closed**: any open question you closed.
4. **Not recorded**: anything you saw in the source and chose not to record, with the reason (it was a question, a suggestion, or not confirmed).
5. **Conflicts**: any disagreement with a standing decision in `PRODUCT.md`.
6. **Lock-in sentence**: one sentence the user can paste back into Slack or Figma so the other person sees it is recorded. Example: `Got it, I've recorded that exports are capped at 500 rows (D-016).` Write the sentence in the language the other person used in the source. If the row is `Pending`, the sentence must ask the other person to confirm. Example: `I've noted the 500-row cap as pending. Can you confirm it's final?`

## Check before you finish

- [ ] The decision is in `design-decisions.md` with an ID and an exact source.
- [ ] No row was deleted.
- [ ] A replaced row has its reason added and its Status changed.
- [ ] `changelog.md` has a new line.
- [ ] The reply ends with one lock-in sentence.
