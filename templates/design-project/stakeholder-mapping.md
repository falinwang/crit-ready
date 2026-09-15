# Stakeholder Mapping

The known-roster reference for this project. `meeting-notes-template.md`'s **👥 Stakeholder Register** section reads from here for name → role/team lookup instead of hardcoding names in the prompt itself. Keep this file current instead of editing the template.

| Name | Team | Function | Notes |
| :--- | :--- | :--- | :--- |
| [Name] | Design | IC | |
| [Name] | Design | IC | |
| [Name] | Product | IC | |
| [Name] | Product | 領導 (Lead) | Final approval authority — see Layer 5 note below |
| [Name] | Engineering | IC | |

## Rules

- **Add a row the first time someone new shows up in a transcript with an identifiable role.** Don't wait for a dedicated cleanup pass.
- **Update Function/Team here if someone's role changes.** Don't leave stale roster entries — a wrong team label produces a wrong attribution in every meeting note that follows.
- **If someone's role is genuinely ambiguous, leave Function blank rather than guessing.** The meeting notes template already has a `TBC` fallback for this — don't pre-fill a guess here that then looks authoritative.
- **This file is per-project.** The same person may have a different role or standing on a different product line — this roster does not travel with them automatically. (If a name is genuinely stable across every project you run, that's a candidate for tracking in the vault-wide `pattern-library.md` as a tag, not for hardcoding into the shared template.)

## Approval / Final-Call Authority

Note here who has final sign-off, so the meeting notes template's "有最終核准權的人是否全程在場" check has something to check against.

- **[Name]** — Product 領導. Flag if absent when a decision touching their area gets made in their absence.
