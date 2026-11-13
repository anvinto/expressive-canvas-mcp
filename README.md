# Expressive Canvas MCP

[![npm version](https://img.shields.io/npm/v/%40anvinto%2Fexpressive-canvas-mcp)](https://www.npmjs.com/package/@anvinto/expressive-canvas-mcp)
[![Node.js version](https://img.shields.io/node/v/%40anvinto%2Fexpressive-canvas-mcp)](https://nodejs.org)

> This repository holds the documentation, the licence and the issue tracker for the npm package
> [`@anvinto/expressive-canvas-mcp`](https://www.npmjs.com/package/@anvinto/expressive-canvas-mcp).
> The source code is not published here.

An MCP server with a living creature on an open canvas in your browser. Your MCP client's model
makes it morph (blob, cat, amoeba, face, bird, robot, or a body it invents), sketch with a pencil,
lay out diagrams and talk. The server holds no model and needs no API key: the model is your
client's. It runs on your own machine and listens on 127.0.0.1 only.

This is a beta (0.x): things may change between minor versions. See `CHANGELOG.md` in the package.

## See it

![A cat draws the loop an agent runs and explains each step](https://media.anvinto.com/expressive-canvas-mcp/0.2.0-beta.2/agentic-workflow.gif)

**A cat explains how an agent works:** goal, plan, act, observe, check, then repeat or finish.

![A blob draws the OAuth authorization code flow with PKCE as a sequence diagram](https://media.anvinto.com/expressive-canvas-mcp/0.2.0-beta.2/oauth-sequence.gif)

**A blob explains OAuth 2.0 with PKCE:** four lifelines and seven numbered messages, one spoken line
each.

Both are scripted: fixed commands replayed through the server's own tools, not a recording of a live
model session.

## Requirements

- Node.js 22 or newer
- A browser (the canvas is a page the server opens at `http://127.0.0.1:18787`)
- An MCP client: Claude Code, Claude Desktop, Cursor, VS Code or Codex

## Install

Claude Code and Claude Desktop are set up by one command each:

```bash
npx -y @anvinto/expressive-canvas-mcp@0.2.0-beta.2 install claude-code
npx -y @anvinto/expressive-canvas-mcp@0.2.0-beta.2 install claude-desktop
```

Restart Claude Desktop after its command. For the other clients, `install` prints the entry to
paste and says which file it goes in:

```bash
npx -y @anvinto/expressive-canvas-mcp@0.2.0-beta.2 install cursor --print
npx -y @anvinto/expressive-canvas-mcp@0.2.0-beta.2 install vscode --print
npx -y @anvinto/expressive-canvas-mcp@0.2.0-beta.2 install codex --print
```

To register it by hand in Claude Code:

```bash
claude mcp add --transport stdio --scope user expressive-canvas -- npx -y @anvinto/expressive-canvas-mcp@0.2.0-beta.2 stdio
```

### Any other MCP client

Any tool that starts MCP servers over stdio can use the canvas. Most of them (Cursor, Windsurf,
Cline, Claude Desktop and others) read a JSON file with an `mcpServers` key. Add this entry to it:

```json
{
  "mcpServers": {
    "expressive-canvas": {
      "command": "npx",
      "args": ["-y", "@anvinto/expressive-canvas-mcp@0.2.0-beta.2", "stdio"]
    }
  }
}
```

Where the file is and what its top key is called differ between clients, so check your client's MCP
documentation. Two that differ:

VS Code (`.vscode/mcp.json`) calls the key `servers` and wants a `type`:

```json
{
  "servers": {
    "expressive-canvas": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@anvinto/expressive-canvas-mcp@0.2.0-beta.2", "stdio"]
    }
  }
}
```

Codex (`~/.codex/config.toml`) uses TOML, and needs longer timeouts because a drawing can run for
minutes:

```toml
[mcp_servers.expressive-canvas]
command = "npx"
args = ["-y", "@anvinto/expressive-canvas-mcp@0.2.0-beta.2", "stdio"]
startup_timeout_sec = 60
tool_timeout_sec = 180
```

If the client cannot find `npx` (some desktop apps start servers with a short `PATH`), give the
full path that `which npx` prints as the `command`.

A client that connects to a URL instead of starting a command can use the server you run yourself.
Start it with `npx -y @anvinto/expressive-canvas-mcp@0.2.0-beta.2 start`, keep it running, and give
the client this entry (Streamable HTTP, this machine only):

```json
{
  "mcpServers": {
    "expressive-canvas": {
      "url": "http://127.0.0.1:18787/mcp"
    }
  }
}
```

Then start a new session in your client and ask, for example:

> Use the canvas to draw how DNS works

The first call opens the canvas in your browser and the drawing starts there.

To choose who presents, say so: "use a red angry bird to explain how an option chain works". To
make it your default, add a line such as "On the canvas, always present as a red angry bird" to
your client's own instructions. To talk to your assistant from the canvas page itself, start the
`present` prompt the server offers: it answers on the board and waits there for your next note or
click until you write "done".

## Commands

Put `npx -y @anvinto/expressive-canvas-mcp@0.2.0-beta.2` in front of each.

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

Run `npx -y @anvinto/expressive-canvas-mcp@0.2.0-beta.2 doctor` first: it names what is wrong and the fix.
If that does not settle it, open an issue at
<https://github.com/anvinto/expressive-canvas-mcp/issues> and attach the file that
`npx -y @anvinto/expressive-canvas-mcp@0.2.0-beta.2 report` writes. It holds versions, the doctor
checks and the end of the log, and no secrets.

## Licence

Copyright (c) 2026 Anvinto FZ-LLC. All rights reserved. This package is free to install and run,
unmodified, for personal and internal business use. It is not open source: see `LICENSE` for the
terms, which are governed by the laws of the United Arab Emirates. The third-party software inside it is listed, each with its own licence, in
`THIRD-PARTY-NOTICES`.
