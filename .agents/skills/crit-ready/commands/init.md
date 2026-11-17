# Init

`/crit-ready init <product>/<project>` creates a new project that belongs to a product.

Example: `/crit-ready init acme-portal/phase-2-reporting`. Here `acme-portal` is the product and `phase-2-reporting` is the project. The two names are names. They are not always a folder path.

This command only makes new projects. To convert a project that already exists, the command is `/crit-ready migrate`.

Do the steps in order.

## Step 1. Find the vault root and read the rules

1. Find the vault root: the folder that has a `templates/` folder directly inside it. If you cannot find it, ask the user where it is.
2. Read the file `templates/shared/RULES.md`. That path starts at the vault root.

## Step 2. Get the two names

1. Write both names in lowercase with hyphens. Example: `Acme Portal` becomes `acme-portal`.
2. If the user gave only one name, ask: "Is `<name>` a new product, or a project inside an existing product? If it is a project, which product?" Wait for the answer.

## Step 3. Decide where the folders go

Check in this order and stop at the first one that gives an answer.

1. The vault's `AGENTS.md`, `CLAUDE.md` or `README.md` says where projects and products live: follow it.
2. The vault already has projects or products: put the new ones in the same kind of place.
3. Neither: put the project folder inside the product folder (`<product>/<project>/`). Ask the user once to confirm: "I'll create `<product>/<project>/` in the vault root. OK?"

## Step 4. Find or create the product

1. Look for this product's `PRODUCT.md`: in the folder where products live, or through the `- **Product:**` link of another project of the same product.
2. Open it and check that it has a "Projects" table and a "Standing Decisions" table.
   - It has both: this is the product file. Use it.
   - It exists but lacks those tables: it belongs to another tool. Do not change it. Ask the user where this product's file should go, and wait.
   - It does not exist: create the product folder, copy `templates/product/PRODUCT.md` into it, and fill in the product name. Fill in the description only from what the user said.
3. If `people.md` is not in the vault root, copy `templates/vault/people.md` there. People are company-wide: a new product does not get its own list.

## Step 5. Check that the project does not exist yet

- The project folder does not exist: go to step 6.
- The project folder exists: do not overwrite anything. Compare it with `templates/design-project/`, tell the user which files are missing, and ask whether to add only those. Then stop. Overwriting `design-decisions.md`, `meeting-notes.md` or a file in `meetings/` would destroy the project's history.

## Step 6. Copy the template

Copy everything in `templates/design-project/` into the new project folder, including the `meetings/` folder. Do not copy the pattern library. It belongs to the whole vault.

## Step 7. Fill in the project's identity

In the new project's `FOLDER-INSTRUCTIONS.md`, fill the four lines under `## Project`:

```
- **Name:** Phase 2 Reporting
- **Product:** Acme Portal ([PRODUCT.md](../PRODUCT.md))
- **Follows:** phase-1-onboarding
- **Status:** Active
```

- The link on the Product line must lead from the project folder to the product's `PRODUCT.md`. Check that it resolves.
- `Follows` is the earlier project of this product, or `none`.

Then add a row to the Projects table in `PRODUCT.md`:

```
| [phase-2-reporting](phase-2-reporting/) | 2 | Active | 2026-03-01 to (ongoing) | Reporting dashboard for account admins |
```

## Step 8. Offer to carry things over

Do this step only if the product has an earlier project.

1. From the earlier project and from `PRODUCT.md`, list:
   - `open-questions.md`: rows in the main table whose Status starts with `Open`.
   - `working-notes.md`: rows in "Deferred & Trade-offs" and "Design System Gaps".
   - `actions.md`: lines under `## Open`.
   - `feedback-tracker.md`: rows with Type `✅ Valid` and Status `Open`.
   - `PRODUCT.md`: rows in "Carried Forward" with nothing in "Picked up by".
2. Show the list to the user. Ask: "Which of these should come into the new project?" Wait.
3. For each item the user picks:
   - Add it to the matching file in the new project. Keep its dates and owner. Add ` (carried from phase-1-onboarding)` to the end of its text, with a link to the file it came from. Its Status in the new project is `Open`.
   - In the place it came from, add ` (carried to phase-2-reporting)` to the end of its text. Do not delete it there and do not change its status.
4. Then ask: "The earlier project has these decisions still `Active`. Do you want any of them to become standing decisions for the product?" For each one the user picks, follow step 3A of `commands/promote.md`.

## Step 9. Check for precedent

1. Find the pattern library: `pattern-library.md` in the vault root, or else `templates/pattern-library.md`.
2. If neither exists, skip this step. Do not create the file.
3. Compare the Tags column with the new project's name and subject.
4. For each real match, tell the user: "A past project (`<origin>`) hit something similar: [pattern]. Outcome: [outcome]. Does that apply here?"
5. If nothing matches, say "no matching precedent found". Do not present a weak match as a match.

## Step 10. Answer the three Kickoff questions

The questions are:

1. What does success look like?
2. How do we measure it?
3. Who is responsible for measuring it?

Do this:

1. Look at what the user already gave you: a brief pasted in the conversation, a ticket, a document near the project folder.
2. For each question that those sources answer, write a draft answer and show it to the user to confirm or change.
3. For each question they do not answer, ask the user.
4. If the user does not know yet, write `TBD (to settle at the Kickoff meeting)`.
5. Never write an answer that is not based on something the user said or wrote.

Write the confirmed answers in the `## Kickoff` section of the new `FOLDER-INSTRUCTIONS.md`.

## Step 11. `NEXT.md`

Look at the other project folders in this vault.

- They have a `NEXT.md`: create one in the new project with the same frontmatter.
- They do not: skip this step.

## Step 12. Write the changelog

In the new project's `changelog.md`, replace the placeholder line with today's date and "Project initialized". If you carried items over, add one more line that says which.

## Step 13. Reply to the user

Tell the user: the path of the new project folder, the product it belongs to, what was carried over, any precedent found, and which Kickoff answers are still `TBD`.

## Check before you finish

- [ ] The project folder has all the template files.
- [ ] The Product link in `FOLDER-INSTRUCTIONS.md` opens the right `PRODUCT.md`.
- [ ] `PRODUCT.md` lists the new project.
- [ ] The three Kickoff answers are filled in or marked `TBD`. None was invented.
- [ ] No existing file was overwritten.
