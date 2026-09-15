---
name: promote-pattern
description: "Use this skill to graduate a local design decision to the cross-project pattern library. Trigger this when the user says /crit-ready promote."
---

# Promote Pattern Skill

When the user asks to promote a pattern (e.g., typing `/crit-ready promote [Decision]. Outcome: [Outcome]. Tags: [Tags]`), perform these steps using file editing tools:

1. **Locate the shared file**: Find `pattern-library.md` located beside the vault's `templates/` directory (it is a vault-wide file, usually at the root of the workspace).
2. **Verify Outcome**: Refuse to promote if there is no known outcome, unless the user explicitly marked it `TBD`. An untested decision is not yet a pattern.
3. **Append**: Add a new row to `pattern-library.md` with today's date, this project's folder name as the Origin Project, the decision, the outcome, the tags, and a relative link back to the source row in this project's `design-decisions.md`.
4. **Do not duplicate rationale**: The row in `pattern-library.md` should link back to the local `design-decisions.md` — it does not restate the full context.
5. **Confirm**: Confirm to the user that the pattern has been added to the global library.
