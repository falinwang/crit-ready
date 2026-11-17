# Stakeholder Mapping

The product-level roster, shared by every project of this product. The **👥 Stakeholder Register** section of `templates/shared/meeting-notes-template.md` reads name-to-role lookups from here instead of hardcoding names in the prompt. Keep this file current instead of editing the template.

Per-project accountability (who owns which call in a given project) stays in that project's `project-brief.md` Roles table. This file records who a person is, not what they own in one project.

| Name | Team | Function | Notes |
| :--- | :--- | :--- | :--- |
| [Name] | Design | IC | |
| [Name] | Design | IC | |
| [Name] | Product | IC | |
| [Name] | Product | 領導 (Lead) | Final approval authority, see Approval / Final-Call Authority below |
| [Name] | Engineering | IC | |

## Rules

- **Add a row the first time someone new shows up in a transcript with an identifiable role.** Do not wait for a dedicated cleanup pass.
- **Update Function and Team here if someone's role changes.** A wrong team label produces a wrong attribution in every meeting note that follows.
- **If someone's role is genuinely ambiguous, leave Function blank rather than guessing.** The meeting notes template already has a `TBC` fallback for this. Do not pre-fill a guess here that then looks authoritative.
- **This file is per-product.** The same person may have a different role or standing on a different product, and this roster does not travel with them automatically.

## Approval / Final-Call Authority

Note here who has final sign-off, so the meeting notes template's check on whether the person with final approval stayed for the whole meeting has something to check against.

- **[Name]**: Product 領導. Flag if absent when a decision touching their area gets made in their absence.
