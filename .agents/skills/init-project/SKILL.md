---
name: init-project
description: "Use this skill to scaffold a new design project folder and initialize the workspace. Trigger this when the user says /crit-ready init or asks to create a new project."
---

# Init Design Project Skill

When the user asks to initialize a project (e.g., typing `/crit-ready init <project-name>`):

1. **Locate the Templates directory**: Find the `templates/` directory containing the `design-project` scaffold. If you can't find it near the current working directory, ask the user where it lives.

2. **Format the Project Name**: Convert the given project name into a lowercase, kebab-case string (e.g., `work-new-feature`).

3. **Check if the project already exists**: Before creating anything, check whether `<project-name>/` is already there. If it is, do NOT blindly overwrite it. Instead, diff it against `templates/design-project/` and offer to fill in only what's missing (e.g. a file added to the template since this project was scaffolded), or ask the user what they want updated. Overwriting an existing project's `design-decisions.md`, `meeting-notes.md`, or any file under `meetings/` (other than `_meeting-template.md` itself) would destroy real project history — treat that as destructive and confirm first.

4. **Create the Folder**: If it doesn't already exist, create a new project directory named `<project-name>/`. If you're unsure where new project folders should live in this workspace, ask the user once — don't guess at a folder-naming convention.

5. **Copy Template**: Copy all files from `templates/design-project/` into the new `<project-name>/` folder, including the `meetings/` subfolder (it should arrive with just `_meeting-template.md` in it — an actual project has no meetings yet). Do NOT copy `templates/pattern-library.md` — it is vault-wide, shared across all projects, and stays where it is.

6. **Create NEXT.md**: Create a `NEXT.md` file in the folder with the standard AI task frontmatter (if applicable to the user's vault rules), setting the AI task state to `inbox`.

7. **Check for Cross-Project Precedent**: Look for `templates/pattern-library.md`. If it does not exist yet, create it from the schema (see the file's own header for the format — it is self-documenting). If it exists, scan its Tags column for anything that overlaps with the new project's name or domain. Surface any matches to the user now, before the Kickoff questions, framed as: "A past project ([Origin Project]) hit something similar — [Pattern] → [Outcome]. Does that precedent apply here, or is this different?" This is a prompt for the user to confirm or dismiss, not an automatic decision. **If nothing overlaps, say so plainly ("no matching precedent found") and move on — do not stretch a loosely-related row into a false match just to have something to surface.**

8. **Draft the Kickoff Answers from existing context first**: Before asking cold, check for anything already on hand that answers the three Kickoff questions below — a brief pasted earlier in the conversation, a ticket link, an existing doc in or near the new project folder. If you find something relevant, draft an answer from it and show the user for confirmation/edits rather than asking them to retype what they already told you. **Do not invent an answer that isn't grounded in something the user actually said or wrote** — an ungrounded guess dressed up as a draft is worse than an honest blank, since it can get accepted without scrutiny.

9. **Ask the Kickoff Questions**: 
   Before finishing, YOU MUST get the user's confirmed answers (drafted or asked fresh) to fill in `FOLDER-INSTRUCTIONS.md`:
   - What does success look like?
   - How do we measure it?
   - Who is responsible for measuring it?

10. **Save Answers**: Once the user confirms, update the new project's `FOLDER-INSTRUCTIONS.md` Layer 4 section with their answers.

Use your filesystem tools (`list_dir`, `run_command`, `write_to_file`) to perform these actions automatically.
