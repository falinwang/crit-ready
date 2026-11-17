# Crit-Ready Rules

The rules every `/crit-ready` skill follows. They live once, here, and are not copied into projects. A project's `FOLDER-INSTRUCTIONS.md` points to this file.

The agent's job is to keep the vault's markdown files as the source of truth for the design workflow: record rationale as given, resolve conflicts by the source priority below, and never invent a reason that nobody stated.

## Scopes

The vault has three scopes. A fact belongs to the narrowest scope that covers it.

| Scope | Files | Holds |
| :--- | :--- | :--- |
| Vault | `pattern-library.md`, `TODAY.md` | Cross-product precedents; the generated daily view |
| Product | `PRODUCT.md`, `stakeholder-mapping.md` | What stays true across phases: standing decisions, domain knowledge, roster, deferred items nobody has picked up |
| Project | everything inside the project folder | One phase or initiative: its decisions, questions, feedback, actions and meetings |

## Layout

The scopes are defined by files and links, not by where folders sit, so a vault keeps whatever organisation it already has.

- **Vault root:** the folder that contains `templates/`. The vault-scope files sit there.
- **Project:** any folder under the vault root that contains a Crit-Ready `FOLDER-INSTRUCTIONS.md`.
- **Product:** the `PRODUCT.md` linked from the Product line of a project's `FOLDER-INSTRUCTIONS.md`. The folder holding that file is the product folder, and the product's `stakeholder-mapping.md` sits beside it. Find a product by following that link. Do not search for files named `PRODUCT.md`, because other tools use the same file name for other things.

Where the vault states its own conventions (in its `AGENTS.md`, `CLAUDE.md` or `README.md`), follow them for where projects and products live. Where it states none, the default is to nest projects inside their product:

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

A vault that keeps active work and long-lived material apart (PARA, for example) can hold projects in one place and products in another. Both layouts work the same way, because the project links to its product.

When a project folder is moved (archived, for example), update the Product link in its `FOLDER-INSTRUCTIONS.md` and its row in the Projects table of `PRODUCT.md`, so the links still resolve.

## Old projects

A skill first reads the project's `FOLDER-INSTRUCTIONS.md`.

- If that file contains its own File Map, the project predates these shared rules. Follow its own File Map, its own copies of the template files, and its own table columns (dates instead of IDs, action items inside meeting files, a pattern library possibly at `templates/pattern-library.md`). Do not convert such a project or add files to it as a side effect of another command. The user converts one by running `/crit-ready migrate`.
- Otherwise, follow this file.

## Locating the project

1. If the working directory is inside a project folder (one that contains `FOLDER-INSTRUCTIONS.md`), use that project.
2. If the user names a project, use it.
3. Otherwise list the project folders and ask which one, but only when more than one is plausible.

A meeting that covers several projects is filed in the project it mostly concerns. Rows for the other project go to that project's own files, with a link back to the meeting file.

## File Map

The meeting notes template (`meeting-notes-template.md`) routes its output by section name. This table is the only place those names resolve to files. If a section name has no row here and is not listed under "Sections with no destination", stop and ask. Do not improvise a destination.

| Routing name | File | Holds |
| :--- | :--- | :--- |
| 🚀 Project Brief | `project-brief.md` | Problem, scope, constraints, definition of done |
| 🗒️ Meeting Notes | this meeting's file in `meetings/` (create it from `meetings/_meeting-template.md` if it does not exist yet, and add a row to `meeting-notes.md`) | One file per meeting: pre-meeting prep and post-meeting notes together. The 👥 Stakeholder Register section fills this file's header |
| ✏️ Design Decisions Log | `design-decisions.md` | Confirmed decisions with ID, rationale and status. If the source names a decider (拍板), record that name in Source / Owner alongside the source |
| ❓ Open Questions | `open-questions.md` | Unanswered questions with urgency and what they block |
| 💬 Feedback Tracker | `feedback-tracker.md` | Stakeholder feedback, typed valid / misunderstanding / preference |
| 📝 Working Notes | `working-notes.md` | Informal log, known gaps, exploratory threads, trade-offs, design system gaps |
| 📦 Deliverables Tracker | `deliverables.md` | What was handed over, to whom, still current or stale |
| ✅ Action Items | `actions.md` | The project's single live action list. The meeting file keeps the same items as plain bullets without checkboxes, as a record |
| 🔗 Reference Links | this meeting's file in `meetings/` | Links to Figma, Jira, PRs and docs discussed. They stay in the meeting file |
| 📅 Changelog | `changelog.md` | Audit trail: one dated line per skill run that writes to the project |

The 👥 Stakeholder Register reads name-to-team lookups from the product folder's `stakeholder-mapping.md`. Keep that roster current instead of editing the notes template. A new person with an identifiable role is added to the roster when first seen.

### Sections with no destination

Do not stop and ask about these four.

- **💡 TL;DR**: a reading aid for the meeting note itself, not project knowledge.
- **🧠 Second Brain Prompt**: belongs to the user's personal knowledge base, not this project. Surface it to the user, never file it.
- **🗂️ Hub Routing**: the list of files actually written to for this meeting. It is a record of routing already done, not content of its own.
- **🧹 0.5 Attribution Cleanup**: a manual to-do for the project owner after the meeting. Leave it in the meeting file.

Every other section must resolve to a row in the File Map.

## Transcript sources

Any transcript source works. The rules care about whether the input is primary speech or someone's summary, not about which tool produced it.

## Source priority

When documents conflict, arbitrate by this order, highest first:

1. **Raw transcript** (primary speech): the definitive source for who said what.
2. **Confirmed meeting file** under `meetings/`, indexed in `meeting-notes.md`: the definitive source for agreed constraints.
3. **Ticket** (Jira, Linear): lagging. If a ticket conflicts with a confirmed meeting decision, the meeting wins and the ticket discrepancy is flagged for the PM.
4. **Slack or Figma comment**: good asynchronous context, but it has to be formalized with `/crit-ready sync` before it counts as a decision.

A meeting file marked `**Source type:** Pre-digested notes` (see `meeting-notes-template.md` Step 0, Mode B) was produced from someone else's summary. Treat it as tier 2 only when nothing else is available. If it conflicts with a file marked `Raw transcript`, the raw transcript wins. Flag the conflict instead of silently trusting the newer or more detailed source.

## IDs

- Each decision gets an ID `D-001`, `D-002`, and so on, unique within its project's `design-decisions.md`. New IDs continue from the highest existing one.
- A reference from another file or another project includes the project folder: `<project>/design-decisions.md` D-012.
- Standing decisions in `PRODUCT.md` use `PD-001`, `PD-002`, and so on, unique within that product.
- `Superseded (→ D-015)` points at an ID, never a date.

## Changelog

Every skill that writes to a project appends one dated line to that project's `changelog.md` saying what was done and which files were touched. Newest at the bottom, same format as the existing lines.

## Precedent check

Before treating a question as new, check:

- `pattern-library.md` at the vault root, for tags matching the situation (bulk-action limits, empty-state ownership, permission edge cases). If a precedent exists, surface it as context ("a past project hit this, here is what happened") rather than re-deriving the trade-off.
- The product's `PRODUCT.md` Standing Decisions. A new decision that contradicts one is flagged to the user. Never edit `PRODUCT.md` to resolve the contradiction on your own.

`/crit-ready init` runs this check for a new project. It can be run any time a decision feels familiar.
