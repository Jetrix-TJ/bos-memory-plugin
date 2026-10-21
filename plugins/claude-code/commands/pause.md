---
description: Pause, resume, or turn off automatic capture (30m, 1h, 1d, 1w, resume, off, on)
argument-hint: "[30m|1h|1d|1w|resume|off|on]"
allowed-tools: Bash(python3:*)
---

!`python3 "${CLAUDE_PLUGIN_ROOT}/bin/bosm-capture" pause $ARGUMENTS`

Tell the person the result above in one line. The switch is theirs, so it applies to every client
they use (other sessions and machines too), not just this session. Do not call any tools.
