# SolveIt Slash Commands

Coding agent harnesses are essentially context engineering tools. They offer different affordances for injecting context into the AI: **slash commands** are direct, human-initiated, on-demand injection; **skills** are on-demand for the agent; **conditional instructions** provide code-based deterministic injection; and **always-on files** like `CLAUDE.md` or `agents.md` are persistent background context.

SolveIt encourages you to engineer the agent's context in a hands-on way, which makes slash commands a natural fit — you're likely to have things you want to tell the agent to do repeatedly.

This repo re-implements slash commands for SolveIt, so you can save reusable prompts and their arguments in structured `.md` files — similar to how `.github/prompts/` works in VS Code with GitHub Copilot.

The implementation just adds a prompt cell to the dialog, so you can review and edit it before executing. It's primarily a time-saver for elaborate prompts you use frequently — refactoring code, creating minimal bug reproductions, "compacting" the dialog by hiding less useful cells, and so on.

This makes SolveIt a little more like Claude Code or GitHub Copilot, but in a very "SolveIt way".

## Setup

Add the `CRAFT.ipynb` from this repo to your SolveIt instance root, and copy the `commands/` folder alongside it. Restart your kernel so the CRAFT runs, and you're ready to go.

## Usage

Type `/command args` in any code cell:

```
/compact
/repro the function raises TypeError when input is None
/simplify the data loading section
/new_command validate run all assertions before committing
```

## Built-in Commands

| Command | Description |
|---|---|
| `/compact` | Hide low-value messages from AI context to free context window |
| `/repro` | Add a new cell with a minimal standalone bug reproduction |
| `/tidy` | Propose dialog reordering/cleanup for sharing |
| `/simplify` | Propose code & dialog simplifications (non-destructive) |
| `/craft` | Generate a CRAFT.ipynb from this dialog's content |
| `/new_command <name> <desc>` | Create a new slash command interactively |

## Variable Substitution

Command `.md` files support these variable patterns:

| Pattern | Expands to |
|---|---|
| `$ARGUMENTS` | Full argument string after the command name |
| `$1`, `$2`, ... | Positional args split by whitespace |
| `@path/to/file` | Contents of that file |
| `` !`shell cmd` `` | stdout of that shell command |

## Adding Your Own

Run `/new_command myname what it does` — the AI will interview you and write `commands/myname.md`.

Or write one directly: any `.md` file in `commands/` with a `description` in its YAML frontmatter is a valid command.

## Notes

- `/compact` uses `update_msg(skipped=1)` — hidden messages can be unhidden anytime via the 👁️ button or `update_msg(id, skipped=0)`
- `/repro`, `/craft`, and `/new_command` add new cells; they never touch existing ones
- `/tidy` and `/simplify` are proposal-only — you stay in control
