# Pi Calm

A standalone Pi extension providing `/calm`: a persistent, quieter terminal conversation view with an animated working boat.

Calm hides the seven wrapped built-in tool calls/results (`read`, `bash`, `edit`, `write`, `grep`, `find`, `ls`), thinking, intermediate assistant notes, and recognized Firstmate operational messages. It keeps substantive final replies. This is presentation only: tools still execute, and session data and model context are not removed. It is not a security or redaction feature. Other extensions' tools and arbitrary custom rows may remain visible.

## Install

Requires Pi (`@earendil-works/pi-coding-agent`) and Git. Pi supplies the TypeScript runtime and peer packages; no build or separate `npm install` is required.

```sh
pi install git:github.com/gzawadzki/pi-calm
```

In an existing interactive Pi session, run `/reload`, then `/calm`. The first invocation enables Calm; the next disables it. Fresh installations default to off.

For project-only installation, use:

```sh
pi install git:github.com/gzawadzki/pi-calm --local
```

Project packages require Pi project trust. Use only one installation scope.

## Installation instructions for an agent

1. Run `pi --version` and `git --version`. If either is missing, report the prerequisite rather than changing the user's environment without permission.
2. Run `pi list` and check for an existing installation. Also inspect the personal extension directory (`~/.pi/agent/extensions`) and, for project installs, `.pi/extensions` for an existing `/calm` registration, particularly `fm-calm.ts`. If a copied or bundled Calm already exists, get approval to disable that copy before installing this package. Two copies can collide on commands and tool definitions; preserve the old files as a backup.
3. Install using the command in **Install** (global by default; `--local` only when requested). Do not copy just `fm-calm.ts`: the `extensions/lib` files and executable shell helper must accompany it.
4. Run `pi list`. Completion requires the Git source to be present and the install command to have exited successfully.
5. Ask the human to run `/reload` (or restart Pi), then `/calm` in the interactive TUI. If this agent has a command context with `ctx.reload()`, it may reload through that API; a shell subprocess cannot reload the parent session. `/calm` is a Pi command, not a shell command.
6. Have the human verify: a normal prompt gets a visible final answer, working activity shows the boat, wrapped built-in tool rows disappear, and toggling `/calm` again restores stock presentation. Report CLI verification separately from human TUI verification; do not claim visual checks that were not performed.

On Windows, Git Bash's `bash` must be on PATH for Firstmate operational-message classification. On Unix, the included helper uses `/usr/bin/env bash`. Core Calm presentation does not require Firstmate itself. If Bash is absent, current typed Firstmate operational messages may remain visible.

## Preferences and compatibility

The toggle is saved at `~/.pi/firstmate-calm/calm` (`on` or `off`) and restored across sessions. Existing Firstmate installations can redirect this via `FM_CONFIG_OVERRIDE`, or via `FM_HOME` / `FM_ROOT_OVERRIDE` (using their `config/calm` file). Installation does not change this preference.

The source records prior verification on Pi 0.81.1, 0.82.0, and 0.84.4; it also contains a queued-row adapter for later Pi APIs. Some presentation adapters patch Pi internals and degrade independently with diagnostics if their APIs change. This is not a guarantee of compatibility with every Pi version. Extensions that replace the same built-in tools can prevent Calm from hiding those rows.

Interactive `/export` and `/share` temporarily request stock rendering to preserve tool detail in exports. Hidden terminal rows are never a promise that exported or persisted content is hidden.

## Update or remove

```sh
pi update git:github.com/gzawadzki/pi-calm
pi remove git:github.com/gzawadzki/pi-calm
```

For project scope, use `--local` on removal. Reload or restart Pi afterward. Removal leaves the preference file intact.

## Origin and license

The extension and support modules were exported from the author's local Pi installation, where they retain the Firstmate `fm-` naming and compatibility hooks. The operational-input shell helper and MIT license were taken from [Firstmate](https://github.com/kunchenguid/firstmate), local checkout commit `050a44643af4f7c9b7a20b1bf165d4834d064c1b`. The exported local TypeScript files are not claimed to be byte-identical to that commit.

Original Firstmate copyright: **2026 Kun Chen**. See [LICENSE](LICENSE).
