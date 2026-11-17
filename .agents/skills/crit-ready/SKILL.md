---
name: crit-ready
description: "Design knowledge coordinator for a UX designer's project vault. Use this skill when the user types /crit-ready followed by init, prep, minutes, sync, promote, today or migrate, or asks to: start a new design project, prepare for a design meeting, process a meeting transcript or meeting notes, log a design decision made in Slack or Figma comments, promote a decision to the product or the pattern library, get today's to-do list across projects, or convert an older Crit-Ready project to the current structure."
---

<!-- argument-hint: init | prep | minutes | sync | promote | today | migrate -->

# Crit-Ready

This skill has seven commands. Each command has its own instruction file in the `commands/` folder, next to this file.

## What to do

1. Find the command word. It is the first word after `/crit-ready`. Example: in `/crit-ready minutes`, the command word is `minutes`.
2. Find that word in the table below.
3. Open the file named in the last column. Read the whole file before you do anything.
4. Do the steps in that file in order, from the first step to the last. Do not skip a step. Do not change the order.
5. Do not open the other command files. You do not need them.

| Command word | The user wants to | File to read |
| :--- | :--- | :--- |
| `init` | Start a new project | `commands/init.md` |
| `prep` | Get ready for a meeting that has not happened yet | `commands/prep.md` |
| `minutes` | File a meeting that already happened (they give a transcript or notes) | `commands/minutes.md` |
| `sync` | Record a decision that was made in Slack, a Figma comment or another chat | `commands/sync.md` |
| `promote` | Keep a decision beyond its project | `commands/promote.md` |
| `today` | See what to do today, across all projects | `commands/today.md` |
| `migrate` | Convert an old-format project to the current format | `commands/migrate.md` |

Everything the user typed after the command word is the input for that command.

## If the user did not type a command word

Match what they asked for to one row:

- They pasted a transcript or meeting notes and want it filed or summarised: use `minutes`.
- They have a meeting coming up and want to prepare: use `prep`.
- They pasted a Slack thread or Figma comments, or said "we decided ...": use `sync`.
- They want a new project set up: use `init`.
- They ask what to do today or for a to-do list: use `today`.

Say which command you are running before you start, in one sentence.

If nothing matches, or two rows match, show the table to the user, ask "Which command do you want?" and stop. Do not guess.

## Rules every command uses

Every command file tells you to read `templates/shared/RULES.md`. That path starts at the vault root. The vault root is the folder that has a `templates/` folder directly inside it. If you cannot find that folder, ask the user where it is.

Three rules matter more than the rest:

1. Never invent a name, a date, a reason or a decision. If the source does not say it, leave the field empty or write `TBD`.
2. Never delete a row from a decisions table. Change its Status. (The example row that a new file starts with is not a real row. `RULES.md` section 11 says when to remove it.)
3. When a step says "stop and ask", stop and ask. Do not continue with a guess.
