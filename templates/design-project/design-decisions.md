# Design Decisions

| ID | Date | Decision | Rationale | Source / Owner | Status | Tags |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| D-001 | YYYY-MM-DD | Example decision | Business or user context | Name (Meeting/Figma) | Active | comma, separated |

**Tags** describe the shape of the problem (e.g. `bulk-action-limits`, `empty-state-ownership`), not the specific fix. They are optional for most rows, but a decision worth flagging for `/crit-ready promote` needs them to be findable later.

**IDs** run `D-001`, `D-002`, and so on within this file. From another file or project, refer to a decision as `<project>/design-decisions.md` D-012.

## Status Values

| Status | Meaning | Usually set by |
| :--- | :--- | :--- |
| `Active` | Currently in effect. The default for a confirmed decision. | Default |
| `Pending` | Recorded but not yet confirmed. Use this when the rationale is missing, the source is unverifiable, or it was said casually rather than agreed. | Agent, during capture |
| `Blocked` | Agreed in principle but held by an external condition (tech constraint, legal, another team). Name the blocker in Rationale. | Agent or user |
| `Superseded (→ D-NNN)` | Replaced by a newer decision. The arrow points to the ID of the row that replaced it. | `/crit-ready sync`, `/crit-ready minutes` |
| `Obsolete` | No longer applies because the underlying problem changed. Keep it as a tombstone. | User |

## Rules

- **Never delete a row.** Change its Status instead. The trail is the point.
- **A decision with no verifiable Source can only be `Pending`.** Do not promote it to `Active` on memory alone.
- **A casual remark is `Pending`, not `Active`.** "I'll just set it to 50 for now" is a proposal until someone owns it.
- **When a decision supersedes a row,** append the reason for the change to the old row's Rationale before changing its Status.
