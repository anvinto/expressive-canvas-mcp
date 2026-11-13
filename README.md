# Expressive Canvas MCP

> This repository holds the documentation, the licence and the issue tracker for the npm package
> [`@anvinto/expressive-canvas-mcp`](https://www.npmjs.com/package/@anvinto/expressive-canvas-mcp).
> The source code is not published here.

An MCP server with a living creature on an open canvas in your browser. Your MCP client's model
makes it morph (blob, cat, amoeba, face, bird, robot, or a body it invents), sketch with a pencil,
lay out diagrams and talk. The server holds no model and needs no API key: the model is your
client's. It runs on your own machine and listens on 127.0.0.1 only.

This is a beta (0.x): things may change between minor versions. The package carries its `CHANGELOG.md`.

## Requirements

- Node.js 22 or newer
- A browser (the canvas is a page the server opens at `http://127.0.0.1:8787`)
- An MCP client: Claude Code, Claude Desktop, Cursor, VS Code or Codex

## Install

Claude Code and Claude Desktop are set up by one command each:

```bash
npx -y @anvinto/expressive-canvas-mcp@0.2.0-beta.1 install claude-code
npx -y @anvinto/expressive-canvas-mcp@0.2.0-beta.1 install claude-desktop
```

Restart Claude Desktop after its command. For the other clients, `install` prints the entry to
paste and says which file it goes in:

```bash
npx -y @anvinto/expressive-canvas-mcp@0.2.0-beta.1 install cursor --print
npx -y @anvinto/expressive-canvas-mcp@0.2.0-beta.1 install vscode --print
npx -y @anvinto/expressive-canvas-mcp@0.2.0-beta.1 install codex --print
```

To register it by hand in any client that starts MCP servers over stdio, the command is `npx` and
the arguments are `-y`, `@anvinto/expressive-canvas-mcp@0.2.0-beta.1`, `stdio`. In Claude Code:

```bash
claude mcp add --transport stdio --scope user expressive-canvas -- npx -y @anvinto/expressive-canvas-mcp@0.2.0-beta.1 stdio
```

Then start a new session in your client and ask, for example:

> Use the canvas to draw how DNS works

The first call opens the canvas in your browser and the drawing starts there.

## Commands

Put `npx -y @anvinto/expressive-canvas-mcp@0.2.0-beta.1` in front of each.

| Command | What it does |
|---|---|
| `start` | Runs the canvas server and opens the page (`--no-open` leaves the browser alone, `--port N` picks the port) |
| `stdio` | MCP over stdio, for clients that start servers themselves; starts the canvas server if none is running |
| `open` | Opens the running canvas in the browser |
| `doctor` | Checks the install, the settings, the server, the tab and the client registrations |
| `install <client>` | Registers the canvas with a client, or prints the entry with `--print` |
| `report` | Writes a bug-report file: versions, the doctor checks, setting names and the end of the log; no secrets |
| `version` | Prints the versions and where this copy was installed from |

Every command takes `--help`.

## Upgrade

The version you run is the one named in your client's entry. To move to another, run `install`
again with that version and `--yes`, then restart the client:

```bash
npx -y @anvinto/expressive-canvas-mcp@<new version> install claude-code --yes
```

## Problems

Run `npx -y @anvinto/expressive-canvas-mcp@0.2.0-beta.1 doctor` first: it names what is wrong and the fix.
If that does not settle it, open an issue at
<https://github.com/anvinto/expressive-canvas-mcp/issues> and attach the file that
`npx -y @anvinto/expressive-canvas-mcp@0.2.0-beta.1 report` writes. It holds versions, the doctor
checks and the end of the log, and no secrets.

## Licence

Copyright (c) 2026 Anvinto FZ-LLC. All rights reserved. This package is free to install and run,
unmodified, for personal and internal business use. It is not open source: see `LICENSE` for the
terms, which are governed by the laws of the United Arab Emirates. The third-party software inside it is listed, each with its own licence, in
`THIRD-PARTY-NOTICES`.
