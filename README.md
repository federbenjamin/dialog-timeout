# dialog-timeout

<p align="center"><strong>Ends a Claude Code turn left waiting on a permission prompt or question for 30 minutes, and tells the agent you are away</strong></p>

<p align="center">
  <a href="LICENSE"><img src="https://img.shields.io/github/license/federbenjamin/dialog-timeout" alt="License"></a>
</p>

A [Claude Code](https://docs.anthropic.com/en/docs/claude-code) plugin for people who leave the agent working while they step away. When the agent stops on a permission prompt or a question and nobody answers, the session sits there for hours. This plugin waits 30 minutes, ends that turn, and sends the agent `automessage: user is /afk`. The `afk` skill that comes with it then has the agent carry on without you instead of waiting.

## Install

Needs Claude Code; tested on 2.1.295.

```
claude plugin install dialog-timeout --marketplace federbenjamin/dialog-timeout
```

It starts in the next interactive session, with a 30-minute timeout.

## Features

- **Unblocks an unattended session.** A permission prompt or question left open for the set time ends the turn. The agent then gets `automessage: user is /afk` as your next message.
- **Comes with the `afk` skill.** It tells the agent to keep working through what is queued, decide what it can, write down the questions only you can answer, and end with a handoff. Run `/dialog-timeout:afk` yourself when you step away.
- **Leaves you alone while you are there.** It only counts while a turn is running and a dialog holds the prompt box. Answer the dialog and the count starts over.
- **One setting for every session.** `/dialog-timeout` changes the minutes, or turns it off, in every open and future session at once.
- **Shows when it acts.** The status line says when it ended a turn, and shows `dialog-timeout off` while it is off.

## Usage

```
/dialog-timeout 10
```

| Command | Effect |
| --- | --- |
| `/dialog-timeout <minutes>` | Set the timeout, in whole minutes, and turn it on |
| `/dialog-timeout off` | Dialogs wait for you, in every session |
| `/dialog-timeout on` | Turn it back on at the last set minutes |
| `/dialog-timeout` | Show the current setting |

## How it works

Every 30 seconds while a turn runs, the plugin asks Claude Code's prompt box whether a dialog holds it. The dialog's age counts from the first check that saw it, so a timeout fires up to 30 seconds late. When the dialog has been open for the set minutes, the plugin ends the turn, closing the dialog unanswered, and submits the away message as you.

- **Headless runs.** `claude -p` and other non-interactive sessions are never touched.

## Contributing

Report a problem or ask a question in [Issues](https://github.com/federbenjamin/dialog-timeout/issues). Pull requests are welcome; see [CONTRIBUTING.md](https://github.com/federbenjamin/.github/blob/main/CONTRIBUTING.md), and report a security issue as [SECURITY.md](https://github.com/federbenjamin/.github/blob/main/SECURITY.md) says.

Run the plugin from a checkout:

```
claude --plugin-dir .
```

Checks, from the repo root:

```
claude plugin test .
tsc -p .
claude plugin validate .
```

`tsc -p .` reads the engine's types from `.claude-plugin/types/`, which Claude Code writes the first time it loads the plugin from this folder (any `claude --plugin-dir .` run).

## License

MIT © Benjamin Feder. See [LICENSE](LICENSE).
