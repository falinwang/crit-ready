# Daily To-Do

`/crit-ready today` writes `TODAY.md` at the vault root, in Traditional Chinese. `TODAY.md` is a generated view. The source files stay the truth, so nothing is typed into `TODAY.md` to stay, except under `## 手動新增`.

## Steps

1. **Read the existing `TODAY.md` first**, if there is one.
   - Items the user ticked there are marked done at their source: tick the matching line in `actions.md` and move it to Done with today's date. In an old project, tick the `- [ ]` in its meeting file.
   - Items the user ticked directly in a project's `actions.md` but that still sit under Open are moved to Done the same way.
   - The `## 手動新增` section is carried over unchanged.
   - Who "I" am comes from a `**我是：** 姓名` line at the top of `TODAY.md`. If it is missing, ask the user once and write the line.

2. **Scan every project** under the vault root (the folder that contains `templates/`). A project is a folder containing `FOLDER-INSTRUCTIONS.md`. Skip projects whose Status is `Paused` or `Shipped`, and folders the vault treats as archived. For a project whose `FOLDER-INSTRUCTIONS.md` has its own File Map (it predates the shared rules, see `templates/shared/RULES.md`), read unticked `- [ ]` items in its meeting files instead of `actions.md`.

3. **Build the list**, grouped by product and project, overdue and soonest first:
   - My open actions.
   - HIGH open questions I own.
   - `Pending` decisions waiting for someone's confirmation.
   - Unaddressed `✅ Valid` feedback.
   - Meetings with prep but no notes, or with attribution cleanup still pending.

4. **Add two short sections:**
   - `等別人`: other people's open actions that block mine.
   - `該回頭看`: Informal Log rows still `Watching` after two weeks, and pattern-library rows whose Outcome is still TBD.

5. **Link every line to its source** (the file and, where possible, the row). Each item is written once, under the project it belongs to.

6. **Write `TODAY.md`.** Put the date and the `**我是：**` line at the top, then the items, then `等別人`, `該回頭看`, and `## 手動新增`. Do not edit any source file other than to mark a ticked item done in step 1.

7. **Reply in chat** with the top few items only (overdue first), and the path of `TODAY.md`.
