---
name: crit-ready
description: "Design knowledge coordinator for a UX designer's project vault. Use this skill when the user types /crit-ready followed by init, prep, minutes, sync, promote, today or migrate, or asks to: start a new design project, prepare for a design meeting, process a meeting transcript or meeting notes, log a design decision made in Slack or Figma comments, promote a decision to the product or the pattern library, get today's to-do list across projects, or convert an older Crit-Ready project to the current structure."
---

<!-- argument-hint: init | prep | minutes | sync | promote | today | migrate -->

# Crit-Ready

One skill, seven commands. Each command's instructions are in its own file under `commands/`, beside this file. Read the file for the command the user asked for and follow it. Read only that file; the others are not needed for the task.

| Command | When | File |
| :--- | :--- | :--- |
| `/crit-ready init <product>/<project>` | Starting a new project | `commands/init.md` |
| `/crit-ready prep [meeting]` | Before a meeting | `commands/prep.md` |
| `/crit-ready minutes` | After a meeting, with a transcript or someone's notes | `commands/minutes.md` |
| `/crit-ready sync [decision] by [who/source]. [reason]. [replaces]` | A decision was made in Slack, Figma comments or another thread | `commands/sync.md` |
| `/crit-ready promote [decision] ...` | A decision should outlive its project | `commands/promote.md` |
| `/crit-ready today` | Building the daily to-do list across projects | `commands/today.md` |
| `/crit-ready migrate [project]` | Converting an older project to the current structure | `commands/migrate.md` |

## Choosing the command

- If the user typed a command, use it. Everything after the command word is that command's input.
- If the user described what they want without naming a command (for example, pasted a transcript and asked for notes), pick the matching command and say which one you are running.
- If the user typed `/crit-ready` alone, or the request fits no command, show the table above and ask what they want. Do not guess.

## Shared rules

Every command works against the vault's shared rules in `templates/shared/RULES.md`: the three scopes (vault, product, project), the layout rules, the File Map, source priority and IDs. Each command file says when to read it. The vault root is the folder that contains `templates/`.
