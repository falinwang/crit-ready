# Pre-Meeting Prep

`/crit-ready prep` builds the prep brief for one upcoming meeting and files it in that meeting's file, so the same file later receives the notes. The approach comes from Tom Greever's *Articulating Design Decisions*; the tactics themselves are in `.agents/skills/greever/cheatsheet.md` and `patterns.md`, so point to them instead of restating them.

## Steps

1. **Find the project and the rules.** Read the project's `FOLDER-INSTRUCTIONS.md`. If it contains its own File Map, the project predates the shared rules: follow its File Map and its own files, and do not add files to it. Otherwise read `templates/shared/RULES.md`.

2. **Get the meeting details.** Take topic, meeting type and attendees from what the user already said. Ask only for what is missing.

3. **Read the matching section** of `templates/shared/pre-meeting-prep.md` for this meeting type. It says what the brief for that type contains.

4. **Read the hub:** `project-brief.md`; the Kickoff answers in `FOLDER-INSTRUCTIONS.md`; decisions made since the last meeting; open questions; unaddressed `✅ Valid` concerns in `feedback-tracker.md`; open items in `actions.md` (in an old project, unticked items in the last meeting's file); the roster in the product's `stakeholder-mapping.md`; and the standing decisions in the product's `PRODUCT.md`.

5. **Create the meeting file** from `meetings/_meeting-template.md` as `YYYY-MM-DD-meeting-name.md`, add a row to `meeting-notes.md`, and fill its Pre-Meeting Prep section with the brief for this meeting type. Leave a field blank where the hub has nothing. Do not guess to fill space. `/crit-ready minutes` will reuse this file after the meeting.

6. **Append a changelog line** to the project's `changelog.md`.

7. **Show the brief** and ask whether the user wants to adjust anything, such as swing votes or the feedback they want and do not want.

## What the brief contains

- **Opening context** in the order Greever describes: the project goal, a one-sentence summary of the last agreement, the current stage, the feedback wanted and not wanted today, and the goal again. Set the goal from `project-brief.md`, and the last agreement from `design-decisions.md` and the previous meeting file.
- **Predicted reactions only for meetings that seek a decision** (Crit, Executive Review). Ground each prediction in that attendee's recorded feedback or informal signals and point to the row. Where the hub has no history for someone, say so. Do not guess from a job title.
- **Tactics that fit this meeting only.** Pick from the cheatsheet and patterns files the few that apply (for example a direct comparison for a Crit, or pre-wiring swing votes for an Executive Review) and name the row or fact that makes each one relevant.
- **Recurring Sync:** a status digest of what changed, what is blocked and which actions are open. It is not a persuasion plan, so skip predictions and tactics.
- **Follow-up:** remind the user to send written decisions and action items within an hour of the meeting, which is what `/crit-ready minutes` produces.
