# BOS Memory for Claude Code

One plugin for everything BOS Memory does in Claude Code:

- **The memory tools** (`get_context`, `recall`, `remember`, `forget`, `check_sources`,
  `report_use`) through the BOS Memory MCP server.
- **Context at the start of every session**: what memory knows about this repository, your rules
  and your open work, given to Claude before your first prompt.
- **Automatic capture**: each turn is sent in the background; after the session the server keeps
  only decisions, commitments, rules, lasting facts and lessons, each citing its turn, and
  deletes the turns.
- **Commands**: `/bos-memory:status`, `:doctor`, `:pause`, `:context`, `:save`, `:recall`.

## Install

You need the server's address and an agent token: on the console's **Connections** page,
choose **Claude Code**. The page shows these commands with both filled in.

In a terminal (Claude Code 2.1.292 or later):

```
claude plugin install bos-memory --marketplace Jetrix-TJ/bos-memory-plugin \
  --config url=https://your-bos-memory-host --config token=bosm_...
```

Or inside Claude Code: `/plugin marketplace add Jetrix-TJ/bos-memory-plugin`, then
`/plugin install bos-memory@bos-memory`; Claude Code asks for the address and the token. The
token is kept in your system keychain.

Then start a new session and run `/bos-memory:doctor`.

If you added BOS Memory before with `claude mcp add`, remove that entry
(`claude mcp remove bos-memory`): the plugin brings the same server.

Needs `python3` (3.9 or later) and `git` on the PATH: macOS, Linux and WSL.

## Hooks

| Hook | Does |
| --- | --- |
| `SessionStart` | Gives Claude what memory knows about this repository and your open work. If the plugin is not set up, or the token was refused, Claude is told how to fix it. |
| `UserPromptSubmit` | Keeps the prompt on this machine until the reply arrives (no network). |
| `Stop` | Queues the prompt and reply as one turn and sends it in the background. |
| `PreCompact` | Sends anything still queued before the context is summarised. |
| `SessionEnd` | Says the session is over, so the server reads it now. |

## Commands

| Command | Does |
| --- | --- |
| `/bos-memory:status` | Connection, capture state, what is waiting on this machine. |
| `/bos-memory:doctor` | Checks Python, git, the address, the token, the server and capture; says how to fix what fails. |
| `/bos-memory:pause [30m\|1h\|1d\|1w\|resume\|off\|on]` | Pause or resume capture everywhere (the same switch as the console). |
| `/bos-memory:context` | What memory knows about the work in this folder. |
| `/bos-memory:save [focus]` | Has Claude save this session's decisions, commitments and rules now. |
| `/bos-memory:recall <question>` | Answers from memory, citing the memories used. |

## Privacy

- Secrets (keys, tokens, passwords, private keys) are stripped on this machine before anything
  is written or sent; the server checks again.
- Pasted text is left out: someone else wrote it.
- A prompt that starts with `#nocapture` is never sent.
- Folders and repositories in the console's "Never capture from" list are checked here, so that
  work never leaves the machine. Local additions: `{"excludes": ["/work/client-x", "acme/*"]}`
  in `~/.bos-memory/config.json`. `BOSM_CAPTURE=off` turns capture off on one machine.
- Turns wait in `~/.bos-memory/spool` while the server cannot be reached (at most 50 MB).
- The hooks keep a copy of the address and token in `~/.bos-memory/credentials.json`, readable
  only by you, so the slash commands reach the same server.
- Captured memories are yours only; admins never see them.

Problems go to `~/.bos-memory/capture.log`; a hook never fails your session.

## Uninstall

`claude plugin uninstall bos-memory`, then delete `~/.bos-memory`.

## Other clients

The capture API is not specific to Claude Code: any tool can send turns to `POST /capture`. The
connection spec is in the console's docs under Reference → Capture API, and the event's JSON
Schema is at `GET /capture/schema`.
