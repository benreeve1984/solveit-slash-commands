# SolveIt Slash Commands

Slash commands for the SolveIt method. Add the CRAFT setup block to your root
`CRAFT.ipynb` to enable them, then use in any code cell:

```
/command args go here
```

## Commands

| Command | Description |
|---|---|
| `/compact` | Hide low-value messages from AI context to free context window |
| `/repro` | Add a new cell with a minimal standalone bug reproduction |
| `/tidy` | Propose dialog reordering/cleanup for sharing |
| `/simplify` | Propose code & dialog simplifications (non-destructive) |
| `/craft` | Generate a CRAFT.ipynb from this dialog's content |
| `/new_command <name> <desc>` | Create a new slash command interactively |

## Variable Substitution in Command Files

| Pattern | Expands to |
|---|---|
| `$ARGUMENTS` | Full argument string after the command name |
| `$1`, `$2`, ... | Positional args split by whitespace |
| `@path/to/file` | Contents of that file |
| `` !`shell cmd` `` | stdout of that shell command |

## Adding Your Own

Run `/new_command myname what it does` and the AI will interview you and write
`~/commands/myname.md` for you.

Or write one directly — any `.md` file in `~/commands/` with a `description`
in its YAML frontmatter is a valid command.

## Notes

- `/compact` uses `update_msg(skipped=1)` — hidden messages can be unhidden
  anytime via the 👁️ button or `update_msg(id, skipped=0)`
- `/repro`, `/craft`, and `/new_command` add new cells; they never touch existing ones
- `/tidy` and `/simplify` are proposal-only — you stay in control
