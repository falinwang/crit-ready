# Init Project

`/crit-ready init <product>/<project>` creates a project that belongs to a product, so projects of one product (phase 1, 2, 3) can share what carries across them. `<product>/<project>` names the two; it is not necessarily a path. This skill creates new projects only. Converting an existing project is `/crit-ready migrate`.

## Steps

1. **Locate the vault root**, the folder that contains `templates/`. If it is not near the working directory, ask the user where it is. Read `templates/shared/RULES.md` for the scopes, the layout rules and the File Map.

2. **Format the names** as lowercase kebab-case (for example `acme-portal/phase-2-reporting`). If the user gave only one name, ask whether it is a new product or a project in an existing one.

3. **Decide where the folders go.** If the vault states its own conventions (in its `AGENTS.md`, `CLAUDE.md` or `README.md`), follow them. Otherwise look at where existing projects and products sit and do the same. If there is nothing to go by, the default is to nest the project inside its product folder; confirm that once with the user.

4. **Resolve the product.**
   - If an existing project of this product links to a `PRODUCT.md`, or a folder for this product already holds a Crit-Ready `PRODUCT.md`, use it.
   - Otherwise create the product folder and copy `templates/product/` into it (`PRODUCT.md` and `stakeholder-mapping.md`), then fill the product name and description from what the user said.
   - A `PRODUCT.md` that lacks the Projects and Standing Decisions tables belongs to another tool. Leave it alone and ask the user where this product's file should go.

5. **Check whether the project exists.** If the project folder is already there, do not overwrite it. Compare it with `templates/design-project/` and offer to add only what is missing. Overwriting `design-decisions.md`, `meeting-notes.md` or any file under `meetings/` other than `_meeting-template.md` destroys project history, so confirm before touching them.

6. **Copy the template.** Copy `templates/design-project/` into the new project folder, including `meetings/` (it arrives with only `_meeting-template.md`). The pattern library is vault-wide and is not copied.

7. **Fill the Project section** of the new `FOLDER-INSTRUCTIONS.md`: name, product (a relative link to its `PRODUCT.md`, wherever that file is), the earlier project it follows (or none), status `Active`. Add a row to the Projects table in `PRODUCT.md`.

8. **Offer to carry over from the earlier project**, if the product has one. Show what could come across and let the user pick:
   - Still-open questions
   - Deferred & Trade-offs and Design System Gaps from its `working-notes.md`
   - Open actions
   - Unaddressed `✅ Valid` feedback
   - Items in `PRODUCT.md` Carried Forward

   Carried items are added to the new project with a link to the origin. The origin is marked as carried (for example "carried to `<project>`"), not deleted. Also offer to promote the earlier project's still-`Active` decisions to standing decisions in `PRODUCT.md`, one at a time, using the same steps as `/crit-ready promote [decision] to product`.

9. **Check for precedent.** Read `pattern-library.md` at the vault root (or `templates/pattern-library.md` if an older setup keeps it there). If none exists, skip this step and do not create one. If it exists, compare its Tags with the new project's name and domain. For each real match, show it before the Kickoff questions: "A past project (`<origin>`) hit something similar: [pattern], outcome [outcome]. Does that apply here?" If nothing matches, say "no matching precedent found" and move on. Do not stretch a loose match.

10. **Draft the Kickoff answers.** Check what is already on hand that answers the three questions (a brief pasted in the conversation, a ticket link, a doc near the folder). Draft answers from that and show them to the user for edits. Never invent an answer. If the user does not know yet, write `TBD (to settle at the Kickoff meeting)`.
   - What does success look like?
   - How do we measure it?
   - Who is responsible for measuring it?

11. **Save the answers** in the Kickoff section of the new `FOLDER-INSTRUCTIONS.md`.

12. **NEXT.md.** Create a `NEXT.md` in the project folder only if other project folders in this vault already have one, and match their frontmatter. Otherwise skip it.

13. **Changelog.** Replace the placeholder line in the new project's `changelog.md` with the initialization date and, if anything was carried over, one line saying what.
