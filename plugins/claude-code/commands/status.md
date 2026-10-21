---
description: Show whether BOS Memory is connected and capturing, and what is waiting to be sent
allowed-tools: Bash(python3:*)
---

!`python3 "${CLAUDE_PLUGIN_ROOT}/bin/bosm-capture" status`

Report this BOS Memory status to the person in three lines or fewer. If something is not set up
or capture is not on, say exactly how to fix it (the output names the fix). Do not call any tools.
