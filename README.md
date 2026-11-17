# Crit-Ready

**English** | [繁體中文](README.zh-TW.md)

**So a designer can always say "why" in a design review.**

Crit-Ready is a set of project knowledge templates and a decision trail for B2B UX designers working with an AI agent (Claude Code or Codex). It is not documentation written for people to read. It is **a second brain for the agent to look things up in**.

---

## 💡 The problems it solves

1. **Decision amnesia**: something gets decided in Slack or out loud in a meeting, the context is lost, and the same discussion happens again.
2. **Sources that disagree**: when Jira, Figma comments and meeting notes conflict, you no longer have to ask around to find out which one is right.
3. **Knowledge that stays in one project**: what you learn on one project becomes a design pattern the team can reuse.

---

## ⚙️ Setup

Crit-Ready has two parts that must sit in the same folder, your **vault** (an Obsidian vault or any folder of markdown notes):

- `templates/`: the file templates and the shared rules. The folder that contains `templates/` is the vault root.
- The `crit-ready` skill: the instructions your agent follows. It lives in `.agents/skills/crit-ready/`.

### Option A: start a new vault

Clone this repository and use it as your vault. Open the folder in Obsidian, and start your agent in it.

```
git clone https://github.com/falinwang/crit-ready.git my-vault
cd my-vault
```

Everything is already in place. `.claude/skills` is a link to `.agents/skills`, so both Claude Code and Codex find the skill.

### Option B: add it to a vault you already have

Copy three things into your vault root:

```
cp -R crit-ready/templates          my-vault/
mkdir -p my-vault/.agents/skills
cp -R crit-ready/.agents/skills/crit-ready crit-ready/.agents/skills/greever  my-vault/.agents/skills/
```

Then, for Claude Code, link its skills folder to the same place:

```
mkdir -p my-vault/.claude
ln -s ../.agents/skills my-vault/.claude/skills
```

Optional: if your vault already has its own folder layout (PARA, for example), say where projects and products live in your vault's `AGENTS.md`. The commands follow it.

### Where each agent looks for skills

| Agent | In the vault | For every folder on your computer | Run a command with |
| :--- | :--- | :--- | :--- |
| Claude Code | `.claude/skills/` | `~/.claude/skills/` | `/crit-ready minutes` |
| Codex | `.agents/skills/` | `~/.agents/skills/` | `$crit-ready minutes` |

You can install the skill in the personal folder instead of the vault. The vault still needs `templates/`, because that is how the skill finds the vault root and the rules.

### Updating

Pull or copy the new `templates/` and `.agents/skills/crit-ready/` over the old ones. This replaces only the templates and the instructions. Your projects, `pattern-library.md` and `TODAY.md` are separate files and are not touched. A project made with an older version keeps working; run `/crit-ready migrate` when you want to convert it.

---

## 🚀 Commands

Every command belongs to one skill, `crit-ready` (`.agents/skills/crit-ready/`), so `/crit-ready` is a real slash command followed by a subcommand:

### 1. `/crit-ready init [product]/[project]` (Project Scaffolding)
Sets up a new project. Several phases of one product (phase 1, 2, 3) belong to the same product and share what the product knows. The agent will:
- Find or create the product (`PRODUCT.md` and `stakeholder-mapping.md`), then copy the project folder structure from `templates/design-project/`. Where the folders go follows your vault's own conventions; only when there are none does the project go inside the product folder.
- **Carry over from the previous phase**: if the product already has an earlier project, it lists what could come across (open questions, deferred items, unfinished actions, valid feedback not yet dealt with) and you pick. Decisions from the earlier phase that still hold can become standing decisions of the product.
- **Check for precedent**: it scans the cross-project pattern library (`pattern-library.md`) and tells you about a related precedent before you start. If there is none, it says "no matching precedent found".
- **Three Kickoff questions**: What does success look like? How do we measure it? Who is responsible for measuring it? The agent drafts answers only from what you have already given it. An answer you do not have yet can be `TBD (to settle at the Kickoff meeting)`.

### 2. `/crit-ready minutes` (Design Knowledge Coordinator)
Give it a meeting transcript, or notes someone else already wrote. It does more than summarise: it files the content into the Hub.
- The notes go into that meeting's own file (the one `/crit-ready prep` created, if there is one), and each section is routed by the File Map to decisions, open questions, feedback, actions and so on.
- **Why, not just what**: every decision carries its rationale and who made the call. A decision with no rationale is filed as `Pending`, with an open question asking for it.
- **Action items** go into the project's `actions.md`, the only list with live checkboxes.
- It replies with a summary you can paste straight into Slack, and a list of what needs you (unclear attribution, suspected reversals, Pending decisions, conflicts with a product standing decision).

### 3. `/crit-ready sync [decision]` (Low-friction Decision Sync)
Turns a scattered discussion in Slack or Figma into a recorded decision:
- Finds the older, conflicting decision in `design-decisions.md` and supersedes it, by decision ID (for example `Superseded (→ D-015)`).
- Closes the matching question in `open-questions.md` and writes follow-up tasks into `actions.md`.
- Produces one confirmation sentence you can paste back into Slack to lock it in.

### 4. `/crit-ready promote` (Pattern Graduation)
Takes a decision that has been tested in practice and keeps it beyond its project. There are two destinations:
- `/crit-ready promote [decision] to product`: makes it a standing decision of the product, written to `PRODUCT.md`. Every later project of that product is reminded of it.
- `/crit-ready promote [decision]. Outcome: [...]. Tags: [...]`: distils a decision and its outcome into the vault-wide `pattern-library.md`, for other products to learn from.

Both run only when you ask. The agent never promotes on its own.

### 5. `/crit-ready prep [meeting name or topic]` (Pre-Meeting Prep)
Before a meeting, it prepares you from what the Hub already holds, following Tom Greever's *Articulating Design Decisions*, and creates the meeting's file:
- **A five-step opening**: it pulls the goal and the last agreement from the project brief, the decisions and the previous meeting, so the meeting starts in the right place.
- **Predicted reactions**: only for meetings that seek a decision (Crit, Executive Review). Each prediction points back to what that attendee said before. Where there is no record, it says so and does not guess from a job title.
- **Only the Greever tactics that fit** (Rule of Direct Comparison, Design Advocates, and so on), not the whole list. A recurring sync gets a status digest and nothing more.

### 6. `/crit-ready today` (Daily To-Do)
Scans every project and writes `TODAY.md` at the vault root:
- Grouped by product and project: my actions, the HIGH open questions I own, Pending decisions waiting for confirmation, valid feedback not yet dealt with, and meetings that have prep but no notes.
- Two more sections, `等別人` (waiting on others) and `該回頭看` (worth a second look), surface what is stuck and what should be revisited.
- `TODAY.md` is a generated view. The real data stays in the source files. An item you tick in `TODAY.md` is written back to `actions.md` on the next run.

### 7. `/crit-ready migrate [project]` (Migrate an Older Project)
Converts a project in the older structure to the current one. One project at a time, and only when you ask:
- It reads the whole project first, lists how each file will change and what it cannot decide by itself, and waits for your approval.
- It backs up the whole project folder before changing anything.
- Decisions get IDs, the to-dos inside meeting files are collected into `actions.md`, and the roster moves up to the product. Existing rows and wording are kept as they are.

---

## 📂 How the knowledge is organised (Log → Link → Lock)

A vault has three scopes: **vault** (across products), **product** (every phase of one product) and **project** (one phase or initiative).

The scopes are defined by files and links, not by where folders sit. A project is any folder that contains a `FOLDER-INSTRUCTIONS.md`, and its product is the `PRODUCT.md` that file links to. So your vault can keep the organisation it already has (PARA, for example, where projects and long-lived material live apart). With no convention of your own, the default layout is:

```
vault/
  templates/            shared/ (rules, kept once), product/, design-project/, vault/ (schemas)
  pattern-library.md    patterns reusable across products
  TODAY.md              daily to-do (generated)
  <product>/
    PRODUCT.md          standing decisions, domain knowledge, deferred items
    stakeholder-mapping.md
    <project>/          one phase or initiative
      FOLDER-INSTRUCTIONS.md, project-brief.md, design-decisions.md, open-questions.md,
      feedback-tracker.md, working-notes.md, deliverables.md, actions.md, changelog.md,
      meeting-notes.md, meetings/
```

The static rules (File Map, source priority, ID rules) live once in `templates/shared/RULES.md` and are not copied into each project. A project in the older structure is never changed automatically, and every command still works on it. To convert one, use `/crit-ready migrate`.

Knowledge settles in three stages: log, link, lock. Every design decision leaves a trail, so none of them becomes a mystery later.

### 1. 📝 Log
**Goal**: capture the informal context, the meeting discussions and the raw ideas, without losing detail.
*   **`meetings/`**: one file per meeting, holding the prep and the notes together. `/crit-ready minutes` structures a messy transcript and files it, so nothing depends on a black-box AI summary.
*   **`working-notes.md`**: your scratchpad for drafts and ideas that have not taken shape yet (Still Exploratory).

### 2. 🔗 Link
**Goal**: turn scattered notes into specific decisions, each tied to its rationale.
*   **`design-decisions.md`**: the centre of the decision trail. Every decision has an ID (`D-001`…), a source and a reason, which ends the "why did we do it this way?" loop.
*   **`open-questions.md`**: tracks what is blocking progress, how urgent it is and what it blocks, with a named owner. A question still open after three meetings is raised with you once, then parked by itself, so old questions that are not yours to answer stop coming back.
*   **`actions.md`**: the project's only action list. Tick an item in Obsidian to complete it.
*   **`/crit-ready sync`**: turns a Slack or Figma conversation into a decision and links it back to the right files.

### 3. 🔒 Lock
**Goal**: make sure the team knows the decision, and promote it into a shared asset once it has proved itself.
*   **`deliverables.md`**: the status of each deliverable (Draft, Handed off, Stale), so engineers do not build from an outdated version.
*   **`PRODUCT.md`**: decisions that stay in force across the phases of one product, locked in with `/crit-ready promote ... to product`.
*   **`pattern-library.md`**: the design pattern library shared across products. `/crit-ready promote` moves a proven decision into it for the whole team.

---

## 🛠️ Daily use

1. Start a project: `/crit-ready init product-name/project-name`.
2. Before a meeting: `/crit-ready prep`. It creates the meeting file and the prep.
3. After a meeting: paste the transcript or notes and type `/crit-ready minutes`. Everything is filed into the project.
4. When something is decided in Slack or Figma: `/crit-ready sync`.
5. Each morning: `/crit-ready today` to see what to do.
6. When a decision proves itself: `/crit-ready promote`.

In Codex, type `$crit-ready` instead of `/crit-ready`.

> **Confidential meetings**: for client, executive or otherwise confidential meetings, check which tools your organisation has approved before you record. Do not use a personal or free-tier AI notetaker. Confirm that its contract lets you opt out of AI model training and that it meets your organisation's compliance bar (SOC 2 / ISO 27001, SSO, data residency), not only that its notes are good.

> *Acknowledgement: the way decisions are articulated here owes a great deal to Tom Greever's* Articulating Design Decisions*. This project takes the idea of "explain it clearly in the room" and extends it into a system where you can also "find it afterwards".*
