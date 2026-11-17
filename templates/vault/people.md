# People

Everyone you work with, one row per person. This file is **company-wide**: it sits once at the vault root, and every product and every project reads it. A person is entered here once, not again for each product.

It records **who a person is**. What they do on one product goes in that product's `PRODUCT.md` (table "People"). What they own in one project goes in that project's `project-brief.md` (table "Roles").

| Name | Also written as | Team | Function | Notes |
| :--- | :--- | :--- | :--- | :--- |
| [Full name] | [Nicknames, short forms, spellings a transcript tool produces] | [Team] | [Function] | [How they work, what they care about] |

## Rules

- **One row per person.** Before adding someone, search the Name and Also written as columns. The same person under two spellings is one row: add the new spelling to Also written as.
- **Add a row the first time someone new appears with a known team or function.** If neither is known, do not add them yet.
- **Leave a cell empty rather than guessing.** A wrong team produces a wrong attribution in every note that follows.
- **Only facts that stay true on every product go here.** "Leads the design team" goes here. "Final say on Acme's checkout" goes in Acme's `PRODUCT.md`. "Owns the export spec in phase 2" goes in that project's `project-brief.md`.
- **Update a row when someone changes team or role.** Do not add a second row.
- **Never delete a row.** Someone who left can say so in Notes.
