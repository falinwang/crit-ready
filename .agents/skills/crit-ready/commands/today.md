# Today

`/crit-ready today` builds the user's to-do list for today, across all projects, and writes it to `TODAY.md` in the vault root.

`TODAY.md` is a view. The real data stays in each project's files. Write `TODAY.md` in Traditional Chinese (Taiwan).

Do the steps in order.

## Step 1. Find the vault root and read the rules

1. Find the vault root: the folder that has a `templates/` folder directly inside it.
2. Read the file `templates/shared/RULES.md`. That path starts at the vault root.

## Step 2. Read the old `TODAY.md`, if there is one

If `TODAY.md` exists in the vault root, read it before you change anything.

1. **Who the user is.** Find the line `**我是：** 姓名`. That name is "me" for the rest of this command.
   - If the file or the line is missing: ask the user "What is your name as it appears in the meeting notes?" and wait.
2. **Ticked items.** For every line that starts with `- [x]`: find the same item in its source file (the link on the line shows which file) and mark it done there. See step 3 for how.
3. **Hand-written items.** Copy everything under the heading `## 手動新增`. You will paste it back unchanged in step 6.

## Step 3. Tidy each project's `actions.md`

For each current project, open `actions.md`.

- A line under `## Open` that starts with `- [x]` was ticked by the user. Move it under `## Done` and add ` | 完成：YYYY-MM-DD` with today's date at the end.
- Do the same for the items you found ticked in `TODAY.md` in step 2.
- Do not tick anything yourself. Only the user decides that something is done.

## Step 4. Find the projects to scan

A project is a folder that has `FOLDER-INSTRUCTIONS.md` directly inside it.

Skip these:

- Anything under `templates/`. The template is not a project.
- A project whose `FOLDER-INSTRUCTIONS.md` says `Status:` `Paused` or `Shipped`.
- Folders the vault treats as archive (the vault's `AGENTS.md`, `CLAUDE.md` or `README.md` says which).

For each project left, check whether it is old: search its `FOLDER-INSTRUCTIONS.md` for the text `templates/shared/RULES.md`. Not found means old.

> **Old project.** It has no `actions.md`. Read the unticked `- [ ]` lines in the Action Items sections of its meeting files. If its instructions name another to-do file (a next-steps file, for example), read that too. If that file is a long backlog, list only the part marked as current, and say how many more items the file has. Its open questions have no Urgency column: list the ones that block the current actions.

## Step 5. Collect the items

For each project, collect these five kinds of item.

| Kind | Where to look | Which rows |
| :--- | :--- | :--- |
| My actions | `actions.md`, under `## Open` | `負責人` is me |
| My urgent questions | `open-questions.md` | Urgency is `HIGH`, Status is `Open`, Owner is me |
| Decisions waiting for confirmation | `design-decisions.md` | Status is `Pending`. Say what is missing (it is in Rationale) |
| Feedback not dealt with | `feedback-tracker.md` | Type is `✅ Valid`, Status is `Open` |
| Meetings not finished | Files in `meetings/` | The file has prep but no notes, or says attribution cleanup is pending |

Then collect two more groups, across all projects.

**等別人 (waiting on others):**

- Open actions owned by someone else that one of my actions depends on.
- Open questions with Urgency `HIGH` that someone else owns.

**該回頭看 (worth a second look):**

- Open actions with no owner (`負責人：TBD`).
- Open actions that look finished but are not ticked. Say why you think so. Do not tick them.
- Rows in the Informal Log of `working-notes.md` that say `Watching` and are older than two weeks.
- Rows in `pattern-library.md` whose Outcome is still `TBD`.

List each item once.

## Step 6. Write `TODAY.md`

Use this layout. Order "my actions" like this: overdue first, then the nearest deadline, then `TBD`.

```
# TODAY — 2026-03-21

**我是：** Mei

> 這份清單由 `/crit-ready today` 產生，資料以各來源檔案為準。在這裡打勾的項目，下次執行時會寫回來源。

## Acme Portal · phase-2-reporting

### 我的行動

- [ ] 更新付款頁的錯誤文案 ｜ 期限：2026-03-22 ｜ [actions.md](acme-portal/phase-2-reporting/actions.md)

### 等待確認的 Pending 決策

- **D-017** 篩選器改成側欄 ｜ 缺：PM 還沒確認

### 尚未處理的有效回饋

- Ken：匯出時沒有進度提示

### 會議

- [2026-03-18 Design crit](acme-portal/phase-2-reporting/meetings/2026-03-18-design-crit.md)：Attribution cleanup 還沒完成

## 等別人

- **Ken**：確認匯出上限對效能的影響 ｜ HIGH

## 該回頭看

- 沒有負責人的行動：「整理元件命名規則」

## 手動新增

```

Rules for this file:

- One `##` heading per project, written as `Product · project-folder`.
- Leave out a `###` heading that has no items.
- Every line links to its source file.
- Paste the hand-written items from step 2 under `## 手動新增`, unchanged.
- Apart from step 3, do not edit any project file in this command.

## Step 7. Reply to the user

In chat, list only the three to five most urgent items, overdue first. Then give the path of `TODAY.md`.

## Check before you finish

- [ ] `TODAY.md` starts with the date and the `**我是：**` line.
- [ ] Nothing under `templates/` or the archive was scanned as a project.
- [ ] You ticked nothing yourself.
- [ ] The hand-written section is unchanged.
- [ ] Each item appears once and has a link.
