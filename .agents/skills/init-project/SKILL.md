---
name: init-project
description: "Use this skill to scaffold a new design project inside a product folder. Trigger this when the user says /crit-ready init <product>/<project> or asks to create a new project."
---

# Init Project

`/crit-ready init <product>/<project>` creates a project folder inside a product folder, so projects of one product (phase 1, 2, 3) can share what carries across them. Only new projects use this structure. Existing projects stay as they are, and this skill never migrates one.

## Steps

1. **Locate the vault root**, the folder that contains `templates/`. If it is not near the working directory, ask the user where it is. Read `templates/shared/RULES.md` for the scopes and the File Map.

2. **Format the names** as lowercase kebab-case (for example `acme-portal/phase-2-reporting`). If the user gave only one name, ask whether it is a new product or a project in an existing one.

3. **Resolve the product.** A product folder is a folder that contains `PRODUCT.md`.
   - If `<product>/` exists with a `PRODUCT.md`, use it.
   - Otherwise create `<product>/` and copy `templates/product/` into it (`PRODUCT.md` and `stakeholder-mapping.md`), then fill the product name and description from what the user said.
   - If no product folder exists anywhere in the vault yet, ask once where product folders should live. Do not guess a convention.

4. **Check whether the project exists.** If `<product>/<project>/` is already there, do not overwrite it. Compare it with `templates/design-project/` and offer to add only what is missing. Overwriting `design-decisions.md`, `meeting-notes.md` or any file under `meetings/` other than `_meeting-template.md` destroys project history, so confirm before touching them.

5. **Copy the template.** Copy `templates/design-project/` into `<product>/<project>/`, including `meetings/` (it arrives with only `_meeting-template.md`). The pattern library is vault-wide and is not copied.

6. **Fill the Project section** of the new `FOLDER-INSTRUCTIONS.md`: name, product (linked to `../PRODUCT.md`), the earlier project it follows (or none), status `Active`. Add a row to the Projects table in `PRODUCT.md`.

7. **Offer to carry over from the earlier project**, if the product has one. Show what could come across and let the user pick:
   - Still-open questions
   - Deferred & Trade-offs and Design System Gaps from its `working-notes.md`
   - Open actions
   - Unaddressed `✅ Valid` feedback
   - Items in `PRODUCT.md` Carried Forward

   Carried items are added to the new project with a link to the origin. The origin is marked as carried (for example "carried to `<project>`"), not deleted. Also offer to promote the earlier project's still-`Active` decisions to standing decisions in `PRODUCT.md`, one at a time, using the same steps as `/crit-ready promote [decision] to product`.

8. **Check for precedent.** Read `pattern-library.md` at the vault root (or `templates/pattern-library.md` if an older setup keeps it there). If none exists, skip this step and do not create one. If it exists, compare its Tags with the new project's name and domain. For each real match, show it before the Kickoff questions: "A past project (`<origin>`) hit something similar: [pattern], outcome [outcome]. Does that apply here?" If nothing matches, say "no matching precedent found" and move on. Do not stretch a loose match.

9. **Draft the Kickoff answers.** Check what is already on hand that answers the three questions (a brief pasted in the conversation, a ticket link, a doc near the folder). Draft answers from that and show them to the user for edits. Never invent an answer. If the user does not know yet, write `TBD (to settle at the Kickoff meeting)`.
   - What does success look like?
   - How do we measure it?
   - Who is responsible for measuring it?

10. **Save the answers** in the Kickoff section of the new `FOLDER-INSTRUCTIONS.md`.

11. **NEXT.md.** Create a `NEXT.md` in the project folder only if other project folders in this vault already have one, and match their frontmatter. Otherwise skip it.

12. **Changelog.** Replace the placeholder line in the new project's `changelog.md` with the initialization date and, if anything was carried over, one line saying what.
