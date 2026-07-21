# Agent Notch

Minimalist macOS notch status for **Claude Code** and **Codex** agents, inspired by @marclou / @edwardluox.

A black window hugs the notch (visible on every space, including fullscreen):

- **Pac-Man chomping (yellow)** beside the notch — at least one agent is currently running
- **Big green circle** — all agents done, time to prompt again
- **Hover** the notch — it expands downward listing recent sessions (running `ᗧ···` / done `●`), with project name, last message snippet, source (Claude/Codex) and age
- **Right-click** — Quit

## How it works

No hooks or APIs — it polls transcript files every 2 s:

- Claude Code: `~/.claude/projects/*/*.jsonl`
- Codex: `~/.codex/sessions/**/*.jsonl`

A session whose transcript was modified in the last 20 s counts as *running*. Sessions idle over 6 h drop off the list.

## Codex pet

The Codex working animation uses the official Codex Pets spritesheets (in `pets/`).
Switch pets with:

```sh
echo dewey > ~/.config/agent-notch/pet
```

Options: `codex`, `dewey`, `fireball`, `rocky`, `seedy`, `stacky`, `bsod`, `null-signal`.
Takes effect within a couple of seconds, no restart needed.

## Build & run

```sh
swiftc -O main.swift -o AgentNotch
./AgentNotch &
```

It is registered as a Login Item (System Settings → General → Login Items → AgentNotch), so it starts automatically. Note: the login item points at the binary's current path — rebuild in place rather than moving it.
