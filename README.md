# BOS Memory plugins

The marketplace for BOS Memory's plugins. Today it has one: **bos-memory**, for Claude Code.

It gives Claude Code your BOS Memory: the memory tools, what memory knows at the start of every
session, automatic capture of the decisions, commitments and rules in your sessions, and the
`/bos-memory:` commands.

## Install

You need your BOS Memory server's address and an agent token. In the BOS Memory console, open
**Connections** and choose **Claude**: the page shows this command with both filled in.

```
claude plugin install bos-memory --marketplace Jetrix-TJ/bos-memory-plugin \
  --config url=https://your-bos-memory-host --config token=bosm_...
```

Claude Code 2.1.292 or later. On older versions, inside Claude Code:
`/plugin marketplace add Jetrix-TJ/bos-memory-plugin`, then `/plugin install bos-memory@bos-memory`,
and enter the address and token when asked.

Then start a new session and run `/bos-memory:doctor`. Update later with
`claude plugin update bos-memory@bos-memory`.

Needs `python3` (3.9 or later) and `git`: macOS, Linux, WSL, and Windows when `python3` runs in a terminal.

Everything else (commands, privacy, uninstalling) is in
[plugins/claude-code/README.md](plugins/claude-code/README.md).

## About this repository

This repository is published automatically from the BOS Memory source; changes made here are
overwritten. Each release is tagged `claude-code-v<version>`.
