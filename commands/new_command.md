---
description: Create a new slash command — usage: /new_command <name> <description>
---
Create a new slash command at ~/commands/$1.md.

Purpose: $ARGUMENTS

Ask me at most 2 brief clarifying questions if needed, covering:
- What inputs it takes (free text, file refs, no args?)
- Whether it should propose changes or apply them directly

Then write the command file following these rules:
- YAML frontmatter with `description`
- `$ARGUMENTS` for full arg string, `$1`/`$2` for positional args
- `@path/to/file` to inject file contents
- `` !`cmd` `` to inject shell output (e.g. `` !`git diff` ``)
- Plain English instructions directed at the AI
- Focused on one clear task
- Prefer proposals over direct edits unless it's explicitly a "do it" command
- fastai style throughout

Save the file, confirm its path, and show a one-line usage example.
