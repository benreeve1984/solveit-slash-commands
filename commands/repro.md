---
description: Add a new cell with a minimal standalone bug reproduction
---
Create a minimal, self-contained bug reproduction and add it as a new code cell.

The repro must:
- Work completely standalone — no references to variables or state from other cells
- Be as short as possible while still triggering the bug
- Include a brief comment: what was expected vs what actually happens
- Follow fastai style: no unnecessary imports, concise names, no boilerplate

Do NOT modify any existing cells. Add the repro as a new code cell using `add_msg`.

$ARGUMENTS
