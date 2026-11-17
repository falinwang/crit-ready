# Crit-Ready Rules

Every `/crit-ready` command follows these rules. This file exists once per vault. It is never copied into a project.

Your job: keep the markdown files in the vault correct. Write down what people decided and why they said they decided it. Never make up a reason, a name, a date or a decision.

## 1. Words

| Word | Meaning | How to recognise it |
| :--- | :--- | :--- |
| Vault root | The top folder of the user's notes | The folder that has a `templates/` folder directly inside it |
| Project | One phase or initiative | Any folder that has a file named `FOLDER-INSTRUCTIONS.md` directly inside it, except folders under `templates/` |
| Product | What several projects belong to | The file `PRODUCT.md` that the project links to (see section 3) |
| Product folder | Where the product's files are | The folder that holds that `PRODUCT.md`. The roster `stakeholder-mapping.md` is in the same folder |
| Hub | The project's files taken together | `design-decisions.md`, `open-questions.md`, `actions.md` and the others listed in section 5 |

## 2. Is this project old or current?

Do this check before writing to any project.

1. Open the project's `FOLDER-INSTRUCTIONS.md`.
2. Search it for the text `templates/shared/RULES.md`.
3. If the text is there, the project is **current**. Follow this file.
4. If the text is not there, the project is **old**. Follow the old-project rules below and ignore sections 5, 7 and 8 of this file.

Old-project rules:

- Use the File Map table inside the project's own `FOLDER-INSTRUCTIONS.md`.
- Use the project's own copies of `meeting-notes-template.md` and `pre-meeting-prep.md`.
- Use the columns the project's tables already have. They have no `ID` column, so do not add IDs. A replaced decision is marked `Superseded (→ YYYY-MM-DD)` with the date of the new row.
- Action items stay in the meeting file as `- [ ]` lines. Do not create `actions.md`.
- The roster is the project's own `stakeholder-mapping.md`. There is no product.
- The pattern library may be at `templates/pattern-library.md`.
- Do not convert the project and do not add new kinds of files to it. Only `/crit-ready migrate` converts a project, and only when the user runs it.

## 3. Where things are

Three scopes. Put each fact in the smallest scope that fits it.

| Scope | Files | What they hold |
| :--- | :--- | :--- |
| Vault | `pattern-library.md`, `TODAY.md` (both at the vault root) | Lessons reusable on other products; the generated daily to-do list |
| Product | `PRODUCT.md`, `stakeholder-mapping.md` (both in the product folder) | What stays true across the product's projects: standing decisions, domain knowledge, the people roster, deferred items nobody has picked up |
| Project | Everything in the project folder | One phase: its decisions, questions, feedback, actions and meetings |

How to find a project's product:

1. Open the project's `FOLDER-INSTRUCTIONS.md`.
2. Find the line that starts with `- **Product:**`.
3. Follow the link on that line. That file is the product's `PRODUCT.md`.

Do not find a product by searching the vault for files named `PRODUCT.md`. Other tools use that file name for other things.

Where folders go:

- If the vault's own `AGENTS.md`, `CLAUDE.md` or `README.md` says where projects and products live, follow it.
- If it says nothing, put each project folder inside its product folder:

```
vault/
  templates/
  pattern-library.md
  TODAY.md
  <product>/
    PRODUCT.md
    stakeholder-mapping.md
    <project>/
      FOLDER-INSTRUCTIONS.md, project-brief.md, design-decisions.md, ...
```

- When a project folder is moved (for example, archived), fix two links: the `- **Product:**` link in its `FOLDER-INSTRUCTIONS.md`, and its row in the Projects table of `PRODUCT.md`.

## 4. Which project?

1. If the folder you are working in is a project, or is inside a project, use that project.
2. Else, if the user named a project, use that project.
3. Else, list the projects in the vault. If there is exactly one, use it. If there are two or more, ask the user "Which project?" and wait for the answer.

If one meeting covers two projects: file the meeting in the project it is mostly about. Rows that belong to the other project go into the other project's files, each with a link back to the meeting file.

## 5. File Map

The meeting notes template produces sections. Each section name below goes to exactly one place. This table is the only place where section names turn into files.

| Section name | Goes to | What that file holds |
| :--- | :--- | :--- |
| 🚀 Project Brief | `project-brief.md` | Problem, scope, constraints, definition of done |
| 🗒️ Meeting Notes | This meeting's file in `meetings/` | One file per meeting: the prep and the notes together |
| 👥 Stakeholder Register | The header of this meeting's file | Who attended. Names and roles are looked up in the product folder's `stakeholder-mapping.md` |
| ✏️ Design Decisions Log | `design-decisions.md` | Decisions with ID, rationale, source and status |
| ❓ Open Questions | `open-questions.md` | Unanswered questions, how urgent, what they block |
| 💬 Feedback Tracker | `feedback-tracker.md` | Stakeholder feedback, typed valid / misunderstanding / preference |
| 📝 Working Notes | `working-notes.md` | Informal log, known gaps, exploratory threads, trade-offs, design system gaps |
| 📦 Deliverables Tracker | `deliverables.md` | What was handed over, to whom, and whether it is still current |
| ✅ Action Items | `actions.md` | The project's only live checklist. The meeting file keeps the same items as plain bullets, without checkboxes |
| 🔗 Reference Links | This meeting's file in `meetings/` | Links to Figma, Jira, PRs and docs discussed. They stay in the meeting file |
| 📅 Changelog | `changelog.md` | One dated line for every command run that changed the project |

Four sections go nowhere. Leave them in the meeting file and do not ask about them:

- **💡 TL;DR**: a reading aid for the note.
- **🧠 Second Brain Prompt**: for the user's personal notes. Show it to the user. Never file it.
- **🗂️ Hub Routing**: the list of files you wrote to for this meeting.
- **🧹 0.5 Attribution Cleanup**: a to-do for the project owner to finish by hand.

Project-specific rows: a project can have routing rows of its own. They are in a table under "Project-specific instructions" in that project's `FOLDER-INSTRUCTIONS.md`. Use them for that project in addition to the table above. They never replace a row above.

**If a section name is not in this table, not in the four above, and not in the project's own rows: stop and ask the user where it goes. Do not invent a file.**

A new person with a known role is added to the product folder's `stakeholder-mapping.md` the first time they appear. If the role is not clear, leave Function empty. Do not guess.

## 6. When two sources disagree

Trust them in this order. 1 beats 2, 2 beats 3, 3 beats 4.

1. **Raw transcript**: the word-for-word record of a meeting. It decides who said what.
2. **Confirmed meeting file** in `meetings/`: it decides what was agreed.
3. **Ticket** (Jira, Linear): often out of date. If a ticket disagrees with a meeting file, the meeting file wins. Tell the user the ticket is out of date.
4. **Slack message or Figma comment**: useful context. It does not count as a decision until the user runs `/crit-ready sync`.

A meeting file marked `**Source type:** Pre-digested notes` was made from someone's summary, not from a transcript. It counts as level 2 only when there is nothing better. If it disagrees with a file marked `Raw transcript`, the raw transcript wins. Tell the user about the disagreement.

It does not matter which tool recorded the meeting. What matters is whether the input is word-for-word speech or someone's summary.

## 7. IDs

- Every decision row in a project's `design-decisions.md` has an ID: `D-001`, `D-002`, `D-003`, and so on.
- To get the next ID: find the highest ID in the table and add 1. If the highest is `D-014`, the next is `D-015`.
- Standing decisions in `PRODUCT.md` use `PD-001`, `PD-002`, and so on, the same way.
- A replaced decision gets the status `Superseded (→ D-015)`, where `D-015` is the ID of the row that replaced it. Use an ID here, never a date.
- When a file outside the project mentions a decision, name the project too: `phase-2-reporting/design-decisions.md` D-012.

## 8. Changelog

Every command that changes a project adds one line at the bottom of that project's `changelog.md`.

- Look at the lines already in the file and copy their format.
- If the file has only the first line, use this format:

```
- **2026-03-04**: minutes: filed "Design crit". Added D-007 and D-008, 2 open questions, 3 actions. Files: meetings/2026-03-04-design-crit.md, design-decisions.md, open-questions.md, actions.md
```

The line says: the date, which command ran, what changed, which files changed. Do not list `changelog.md` itself among the files.

## 9. Has this come up before?

Before treating a design question as new, check two places:

1. `pattern-library.md` at the vault root. Compare its Tags column with the situation. If a row matches, tell the user: "A past project hit this: [pattern], outcome: [outcome]."
2. The Standing Decisions table in the product's `PRODUCT.md`. If a new decision disagrees with a row there, tell the user. Do not edit `PRODUCT.md` to fix it.

If nothing matches, say "no matching precedent found". Do not present a weak match as a match.

## 10. Rules that always apply

- Never delete a row from `design-decisions.md`, `PRODUCT.md` or `pattern-library.md`. Change its Status instead.
- Never invent content to fill an empty field. Leave it empty or write `TBD`.
- Never rewrite a past meeting file to match a later decision. Record the change in `design-decisions.md`.
- A new project's files contain example rows, such as a row full of `YYYY-MM-DD`, `[Name]` or the word `Example`. They show the format. They are not data. The first time you add a real row to a table or list, delete its example row. Never count an example row, never link to it, and never treat it as a decision.
- When you are not sure, stop and ask the user. A question costs less than a wrong row.
