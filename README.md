# Memgraph plugins

Plugins that help AI coding agents build with [Memgraph](https://memgraph.com).
One repository for every agent: Claude Code, Codex, Hermes and others.

> **Proof of concept.** The layout and install commands are being tested. Skills
> are copied from [memgraph/skills](https://github.com/memgraph/skills) (`fa356b3`)
> and are not edited here yet.

## Plugins

| Plugin | What it adds | Lives in |
| --- | --- | --- |
| `memgraph` | Skills for Cypher, data modeling, import, indexes, configuration, MAGE algorithms, query modules, mgconsole and GraphRAG; the Memgraph docs MCP server; the Memgraph MCP server for your database (read-only by default) | [`memgraph/`](memgraph) |
| `context-graph` | AI Memory: records your agent sessions into Memgraph Context Graph and recalls them later. Needs the `memgraph-context-graph` CLI | [memgraph/ai-toolkit](https://github.com/memgraph/ai-toolkit/tree/main/context-graph/plugins) |

## Install

| Agent | Command |
| --- | --- |
| Claude Code | `/plugin marketplace add memgraph/plugins`, then `/plugin install memgraph@memgraph` |
| Codex | `codex plugin marketplace add memgraph/plugins`, then install `memgraph` from the plugin directory |
| Hermes and other [Agent Plugins](https://agent-plugins.org) agents | `hermes plugins install memgraph/plugins/memgraph` |
| Other agents (skills only) | `npx skills add memgraph/plugins` |

The Memgraph MCP server runs with `uvx`, so it needs [uv](https://docs.astral.sh/uv/).
It connects to `bolt://localhost:7687` unless you set `MEMGRAPH_URL`.

## Layout

```
.claude-plugin/marketplace.json   Claude Code catalog
.agents/plugins/marketplace.json  Codex catalog
memgraph/
  plugin.json, mcp.json           Agent Plugins 1.0 (Hermes and others)
  .claude-plugin/plugin.json      Claude Code
  .codex-plugin/plugin.json       Codex
  .mcp.json                       MCP servers for Claude Code and Codex
  skills/                         Agent Skills
```
