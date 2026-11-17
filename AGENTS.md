# AGENTS.md

This file provides guidance to AI coding agents (Claude Code, Codex) when working in this repository. `CLAUDE.md` imports it, so edit this file, not that one.

## What this repo is

Crit-Ready is not an application. It is a set of markdown templates and agent skills that turn an AI agent into a **Design Knowledge Coordinator** for a UX designer's vault (Obsidian or similar). It tracks a project from kickoff through every meeting to a daily to-do list, and extends from one project to several projects of one product (phase 1, 2, 3) and across products. There is no build, lint, or test tooling; all work here is editing prompt/template markdown files. See `README.md` for the full pitch and mechanism list.

## Repository structure

The user's vault has three scopes. The vault root is the folder containing `templates/`.

```
vault/
  templates/            shared/, product/, design-project/, vault/
  pattern-library.md    live, vault-wide (created from templates/vault/pattern-library.md)
  TODAY.md              generated daily to-do across all projects
  <product>/            a folder containing PRODUCT.md
    PRODUCT.md, stakeholder-mapping.md
    <project>/          a folder containing FOLDER-INSTRUCTIONS.md (one phase or initiative)
```

- **`templates/shared/`** — static rules, kept once and never copied into projects:
  - `RULES.md` — the three scopes, the old-project compatibility rule, how to locate the project, the **File Map** (routing table from meeting-notes section names to destination files; the only place those names resolve), sections with no destination, source-priority order, ID rules, changelog rule, precedent check.
  - `meeting-notes-template.md` — the prompt to run over a transcript or someone else's pre-digested notes. Mode A (raw transcript, full pipeline) vs Mode B (second-hand summary, don't reconstruct attribution or content the source lacks). Output sections route per the File Map.
  - `pre-meeting-prep.md` — static reference guide (Traditional Chinese) for six meeting types. The actual brief for a meeting is copied into that meeting's file.
- **`templates/product/`** — copied by `/crit-ready init` into a new product folder: `PRODUCT.md` (standing decisions `PD-NNN`, domain knowledge, projects table, carried-forward items) and `stakeholder-mapping.md` (the product-level roster).
- **`templates/design-project/`** — copied into `<product>/<project>/`: `FOLDER-INSTRUCTIONS.md` (short: project, pointer to shared rules, Kickoff questions), `project-brief.md`, `design-decisions.md` (ID column `D-NNN`), `open-questions.md`, `feedback-tracker.md`, `working-notes.md`, `deliverables.md`, `actions.md` (the single live action list), `changelog.md`, `meeting-notes.md` (index only), `meetings/_meeting-template.md` (one file per meeting, prep and notes together).
- **`templates/vault/pattern-library.md`** — schema for the live vault-root `pattern-library.md`. Never copied into a product or project. Do not duplicate its schema elsewhere.
- **`.agents/skills/`** — one skill per command: `init-project` (`/crit-ready init <product>/<project>`), `magic-minutes` (`minutes`), `pre-meeting-prep` (`prep`), `sync-decision` (`sync`), `promote-pattern` (`promote`), `daily-todo` (`today`). `greever/` is a separate knowledge base the prep skill points to.

## Key mechanics to preserve when editing

- **Old-project compatibility.** Only new projects use this structure. Every skill first reads the project's `FOLDER-INSTRUCTIONS.md`; if it contains its own File Map, the project predates the shared rules and the skill follows that project's own File Map, files and table columns (dates instead of IDs, action items in meeting files, pattern library possibly at `templates/pattern-library.md`). Never migrate it or add files to it unless asked. Keep this rule in `RULES.md` and in each skill's first step.
- **File Map changes.** If you add a new routing name to `meeting-notes-template.md`'s Sections, you must also add its destination to the File Map in `templates/shared/RULES.md`. An unmapped section name is meant to make the agent stop and ask, not improvise.
- **`/crit-ready minutes`** finishes when the hub is updated: notes written to the meeting file, sections routed, action items into `actions.md`, changelog line appended. Running it twice on one meeting updates rows rather than duplicating them.
- **`/crit-ready sync [Decision] by [Who/Source]. [Reason]. [Replaces]`** supersedes conflicting rows (`Superseded (→ D-NNN)`), closes matching open questions, flags conflicts with `PRODUCT.md` standing decisions, and produces a one-sentence Slack-pasteable confirmation.
- **`/crit-ready promote`** has two targets: `... to product` (Standing Decision in `PRODUCT.md`) and `... Outcome: [...]. Tags: [...]` (vault-root `pattern-library.md`, refuses without an Outcome or explicit `TBD`). Links back to the origin row rather than duplicating rationale. Human-triggered only.
- **Never delete a row** in `design-decisions.md`, `pattern-library.md` or `PRODUCT.md`. Status changes (`Superseded`, `Obsolete`) preserve the trail.
- **Skills never edit `PRODUCT.md` on their own** to resolve a conflict with a standing decision; they flag it to the user.
- **`actions.md` is the only live checklist.** Meeting files keep action items as plain bullets. `TODAY.md` is a generated view, and ticks made there are written back to `actions.md` on the next `/crit-ready today`.
- Keep `meeting-notes-template.md` tool-agnostic (no list of vendor names) and keep its Mode A / Mode B behavior intact.
- Skill text is plain English: say what to do and why, no personas, no emoji, no tool names from other harnesses.

## Language conventions

Section headers in `meeting-notes-template.md` stay in English; the meeting note content itself is written in Traditional Chinese (Taiwan). `README.md`, `pre-meeting-prep.md`, `actions.md` item wording and `TODAY.md` are Traditional Chinese. `RULES.md`, `PRODUCT.md`, the other project templates and the skills are English. Match the existing language of whichever file you're editing.
