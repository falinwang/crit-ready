# Promote

`/crit-ready promote` copies a decision to a place where it outlives its project.

Only the user starts a promotion. Never promote a decision because it looks reusable. Never promote as a side effect of another command.

There are two destinations. Look at what the user typed to know which one.

| The user typed | Destination | What it means |
| :--- | :--- | :--- |
| `/crit-ready promote [decision] to product` | The product's `PRODUCT.md`, table "Standing Decisions" | The decision stays in force for the product's later projects |
| `/crit-ready promote [decision]. Outcome: [...]. Tags: [...]` | `pattern-library.md` at the vault root | A lesson that a designer on another product could reuse |

If you cannot tell which one the user wants, ask "Promote to the product, or to the pattern library?" and stop.

Do the steps in order.

## Step 1. Find the project and the rules

1. Find the vault root: the folder that has a `templates/` folder directly inside it.
2. Find the project. A project is a folder with a `FOLDER-INSTRUCTIONS.md` in it.
   - If you are working inside a project folder, use it.
   - Else, if the user named a project, use it.
   - Else, list the projects. If there is one, use it. If there are several, ask "Which project?" and wait.
3. Open the project's `FOLDER-INSTRUCTIONS.md`. Search it for the text `templates/shared/RULES.md`.
   - Found: the project is **current**. Read the file `templates/shared/RULES.md` now. That path starts at the vault root.
   - Not found: the project is **old**. It has no product and no decision IDs. "To product" is not possible: tell the user to run `/crit-ready migrate` first, and stop. Promotion to the pattern library still works: refer to the decision by its date.

## Step 2. Find the decision row

Open the project's `design-decisions.md`. Find the row the user means, by its ID or by its words.

- One row matches: use it.
- If that row's Status is `Pending`, `Superseded` or `Obsolete`: tell the user the status and ask "Promote it anyway?" Stop and wait. An unconfirmed or replaced decision should not outlive its project by accident.
- No row matches, or several match: show the candidates, ask "Which one?" and stop.

Then go to step 3A or step 3B.

## Step 3A. Promote to the product

1. Open the project's `FOLDER-INSTRUCTIONS.md`. Find the line that starts with `- **Product:**`. Follow its link to `PRODUCT.md`.
   - If there is no such line or the file does not exist: tell the user and stop. Do not create a `PRODUCT.md` here.
2. Read the Standing Decisions table.
   - If a row already says the same thing: tell the user and stop.
   - If a row disagrees with this decision: show both to the user and ask which one stands. If the new one replaces the old one, set the old row's Status to `Superseded (→ PD-NNN)` after you add the new row.
3. Add a row at the bottom of the table. If the table holds only the example row, replace it (see `RULES.md` section 11).
   - **ID**: the highest `PD-` number among real rows plus 1. Ignore the example row. With no real rows, use `PD-001`.
   - **Decision**: the decision, in one sentence.
   - **Origin**: a link to the project's `design-decisions.md`, followed by the decision ID.
   - **Since**: today.
   - **Status**: `Active`.

   Example:

   ```
   | PD-004 | 匯出一次最多 500 筆 | [phase-2-reporting/design-decisions.md](phase-2-reporting/design-decisions.md) D-016 | 2026-03-20 | Active |
   ```
4. Do not copy the rationale. The link leads to it. No Outcome is needed.

Go to step 4.

## Step 3B. Promote to the pattern library

1. **Check the Outcome.** The user must give an Outcome: what really happened after the decision shipped.
   - No Outcome given: refuse. Say "A decision with no known result is not a pattern yet. Give me the Outcome, or write `Outcome: TBD` if it is too early to tell." Stop.
   - The user wrote `Outcome: TBD`: continue.
2. **Find the library file.** Look in this order:
   1. `pattern-library.md` in the vault root. If it exists, use it.
   2. `templates/pattern-library.md`. If it exists, use it. Do not make a second one.
   3. Neither exists: copy `templates/vault/pattern-library.md` to `pattern-library.md` in the vault root, and use that.
3. **Add a row** at the bottom of the table. Use the columns the file's header row has.
   - **Date Promoted**: today.
   - **Pattern / Trade-off**: a short name for the situation.
   - **Origin**: the product and project, the decision ID, and a link to the project's `design-decisions.md`.
   - **Decision Made**: the decision, in one sentence.
   - **Outcome**: what the user gave.
   - **Tags**: the tags the user gave. Tags name the situation, not the fix.
   - **Reusable When**: the condition under which this lesson applies. If the user did not say, write `TBD` and tell the user in step 5 that this cell needs them.

   Example:

   ```
   | 2026-03-20 | 大量匯出的上限 | acme-portal/phase-2-reporting D-016 ([link](../acme-portal/phase-2-reporting/design-decisions.md)) | 匯出一次最多 500 筆 | 上線後逾時回報歸零，兩位客戶要求提高上限 | bulk-action-limits | 匯出或批次操作會拖慢頁面時 |
   ```
4. Do not copy the rationale. The link leads to it.
5. Never delete a row. If a later project proves a pattern wrong, add a new row that says so.

## Step 4. Write the changelog line

Add one line at the bottom of the project's `changelog.md`. Copy the format of the lines already there. It says: the date, `promote`, which decision, where it went.

## Step 5. Reply to the user

Say what you added, with its ID if it has one, and the path of the file you added it to.

## Check before you finish

- [ ] The user asked for this promotion.
- [ ] For the pattern library: there is an Outcome, or the user wrote `TBD`.
- [ ] The new row links back to the project's decision. The rationale was not copied.
- [ ] No row was deleted.
- [ ] `changelog.md` has a new line.
