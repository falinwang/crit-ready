---
name: sync-decision
description: "Use this skill to log an asynchronous design decision (from Slack, Figma, etc.). Trigger this when the user says /crit-ready sync."
---

# Sync Design Decision Skill

When the user asks to sync a decision (e.g., typing `/crit-ready sync [Decision] by [Who/Source]. [Reason]. [Replaces]`), perform these steps using file editing tools:

1. **Search & Supersede**: Open `design-decisions.md` in the current project. If the new decision explicitly replaces an old one, or obviously conflicts with one, mark the old row's Status as `Superseded (→ YYYY-MM-DD)` (pointing to today) and append the new reason for the change to the old row's Rationale.
2. **Record**: Add the new decision to `design-decisions.md` as a new row with today's date, the source, and the rationale. Set its Status to `Active`.
3. **Clear**: Check `open-questions.md`. If this sync resolves an open question, mark it as `[CLOSED]` with today's date as the last confirmed date.
4. **Lock-in Phrase**: Output a 1-sentence confirmation phrase that the user can copy-paste into Slack/Figma to "Lock in Agreement" with the stakeholder (e.g., "Got it, I've recorded that...").
