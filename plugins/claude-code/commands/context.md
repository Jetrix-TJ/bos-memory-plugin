---
description: Show what BOS Memory knows about the work in this repository
allowed-tools: Bash(python3:*)
---

!`python3 "${CLAUDE_PLUGIN_ROOT}/bin/bosm-capture" show-context`

Show the person what BOS Memory knows, grouped as it is above (rules, open items, people and
projects, relevant). Keep each item to one line and keep the memory ids. If nothing is known yet,
say so in one line.
