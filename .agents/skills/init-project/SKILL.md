---
name: init-project
description: "Use this skill to scaffold a new design project folder and initialize the workspace. Trigger this when the user says /init or asks to create a new project."
---

# Init Design Project Skill

When the user asks to initialize a project (e.g., typing `/init <project-name>`):

1. **Format the Project Name**: Convert the given project name into a lowercase, kebab-case string (e.g., `work-new-feature`).
2. **Create the Folder**: Create a new directory in `10-projects/<project-name>/`. (If it needs a specific area prefix like `work-` or `rw-`, ensure it's added as per `AGENTS.md` rules).
3. **Copy Template**: Copy all files from `templates/design-project/` into `10-projects/<project-name>/`.
4. **Create NEXT.md**: Create a `NEXT.md` file in the folder with the standard AI task frontmatter, setting the AI task state to `inbox`.
5. **Ask the Kickoff Questions**: 
   Before finishing, YOU MUST ask the user the three Kickoff questions to fill in `FOLDER-INSTRUCTIONS.md`:
   - What does success look like?
   - How do we measure it?
   - Who is responsible for measuring it?
6. **Save Answers**: Once the user answers, update the `<project-name>/FOLDER-INSTRUCTIONS.md` Layer 4 section with their answers.

Use the `run_command` and `write_to_file` tools to perform these actions automatically for the user.
