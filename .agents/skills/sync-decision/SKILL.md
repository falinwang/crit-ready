---
name: sync-decision
description: "Use this skill to log an asynchronous design decision (from Slack, Figma comments, etc.). Trigger this when the user says /crit-ready sync, with or without decision text."
---

# Sync Design Decision Skill

Typical invocation: `/crit-ready sync [Decision] by [Who/Source]. [Reason]. [Replaces]`. The decision text may also be missing, in which case use the source from the current conversation (see "No decision text given").

## Before editing

1. Read the project's `FOLDER-INSTRUCTIONS.md` (File Map and source-priority rules) and the header, Status Values and Rules sections of `design-decisions.md`. Use the table's actual columns. Do not assume them.
2. Figma comments and Slack are tier 4 sources. `/crit-ready sync` is what formalizes them, so always cite the platform, the person, and the date in Source / Owner. If the source tags a Decider, record that name too.

## No decision text given

Look for a source earlier in this conversation (Figma comments, Slack thread, pasted text) and extract only decisions that were actually concluded: a resolved thread, an explicit confirmation from the owner, or an agreement between named people.

- Do NOT log open questions, suggestions or reviewer asks as decisions. List them to the user as unlogged instead.
- If nothing in the conversation qualifies, ask the user what to sync. Do not invent one.

## Steps

1. **Search & Supersede**: Search `design-decisions.md` for overlapping rows first (grep on key terms). If the new decision explicitly replaces or obviously conflicts with an old one, append the reason for the change to the old row's Rationale first, then set its Status to `Superseded (→ YYYY-MM-DD)` pointing to the new row's date. If a matching row already exists, update it rather than adding a duplicate. Never delete a row.
2. **Record**: Append the new row after the last table row, with today's date, the source, the rationale and tags (tags describe the shape of the problem, reuse existing tags where they fit). Choose Status by the hub's own rules:
   - `Active`: confirmed by a verifiable source and owned by someone (the owner, Product, or the people the thread agreed on).
   - `Pending`: one person's proposal, a casual remark, or no explicit sign-off from the owner. Say in Rationale what confirmation is missing.
   - `Blocked`: agreed in principle but held by an external condition, named in Rationale.
3. **Clear**: Check `open-questions.md`. If this sync resolves an open question, strike through its question text, add `**[CLOSED] M/D:**` with the resolution, set the last-confirmed date to today, and move the row to the 已結案 (Closed / Resolved) section. If it only partly answers one, add a dated update to that row and leave it open. Keep that file's language (Traditional Chinese) and its row format.
4. **Report**: Tell the user what was added, superseded and closed, and list anything seen in the source but deliberately not logged (open questions, unresolved asks) with why.
5. **Lock-in Phrase**: Output one sentence the user can paste into Slack/Figma to lock in agreement with the stakeholder (e.g. "Got it, I've recorded that..."). If any logged row is `Pending`, the phrase should ask the stakeholder to confirm it.
