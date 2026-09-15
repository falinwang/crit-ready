---
name: init-project
description: "Use this skill to scaffold a new design project folder and initialize the workspace across any PARA vault structure. Trigger this when the user says /init or asks to create a new project."
---

# Init Design Project Skill

When the user asks to initialize a project (e.g., typing `/init <project-name>`):

1. **Detect the PARA Structure**: 
   - Use your tools to list the root directory and find the active **Projects** directory (it might be named `10-projects`, `1-Project`, `Projects`, `01-Projects`, etc.).
   - Find the **Templates** directory containing the `design-project` scaffold (it might be named `templates`, `Templates`, `00-Templates`, etc.).
   *Note: If you cannot confidently determine the locations, ask the user to clarify their PARA folder names.*

2. **Format the Project Name**: Convert the given project name into a lowercase, kebab-case string (e.g., `work-new-feature`).

3. **Create the Folder**: Create a new directory in `<Projects-Dir>/<project-name>/`. (If the user's specific vault rules require an area prefix like `work-`, apply it).

4. **Copy Template**: Copy all files from `<Templates-Dir>/design-project/` into `<Projects-Dir>/<project-name>/`. Do NOT copy `<Templates-Dir>/pattern-library.md` — it is vault-wide, shared across all projects, and stays where it is.

5. **Create NEXT.md**: Create a `NEXT.md` file in the folder with the standard AI task frontmatter (if applicable to the user's vault rules), setting the AI task state to `inbox`.

6. **Check for Cross-Project Precedent**: Look for `<Templates-Dir>/pattern-library.md`. If it does not exist yet, create it from the schema (see the file's own header for the format — it is self-documenting). If it exists, scan its Tags column for anything that overlaps with the new project's name or domain. Surface any matches to the user now, before the Kickoff questions, framed as: "A past project ([Origin Project]) hit something similar — [Pattern] → [Outcome]. Does that precedent apply here, or is this different?" This is a prompt for the user to confirm or dismiss, not an automatic decision.

7. **Ask the Kickoff Questions**: 
   Before finishing, YOU MUST ask the user the three Kickoff questions to fill in `FOLDER-INSTRUCTIONS.md`:
   - What does success look like?
   - How do we measure it?
   - Who is responsible for measuring it?

8. **Save Answers**: Once the user answers, update the `<Projects-Dir>/<project-name>/FOLDER-INSTRUCTIONS.md` Layer 4 section with their answers.

Use your filesystem tools (`list_dir`, `run_command`, `write_to_file`) to dynamically find the paths and perform these actions automatically.
