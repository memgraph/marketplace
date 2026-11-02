# Memgraph plugin marketplace

Catalogs of plugins that help AI coding agents build with [Memgraph](https://memgraph.com).
This repository holds only the catalogs; each plugin lives in the repository where its code is.

> **Proof of concept.** The `memgraph` entry points at the `poc/plugins-catalog` branch of
> memgraph/skills. The earlier layout, with the plugin copied into this repository, is tagged
> [`poc-folder-layout`](../../tree/poc-folder-layout).

## Plugins

| Plugin | What it adds | Lives in |
| --- | --- | --- |
| `memgraph` | Skills for Cypher, data modeling, import, indexes, configuration, MAGE algorithms, query modules, mgconsole and GraphRAG; the Memgraph docs MCP server; the Memgraph MCP server for your database (read-only by default) | [memgraph/skills](https://github.com/memgraph/skills) |
| `context-graph` | AI Memory: records your agent sessions into Memgraph Context Graph and recalls them later. Needs the `memgraph-context-graph` CLI | [memgraph/ai-toolkit](https://github.com/memgraph/ai-toolkit/tree/main/context-graph/plugins) |

## Install

| Agent | Command |
| --- | --- |
| Claude Code | `/plugin marketplace add memgraph/marketplace`, then `/plugin install memgraph@memgraph` |
| Codex | `codex plugin marketplace add memgraph/marketplace`, then install `memgraph` from the plugin directory |
| Other agents (skills only) | `npx skills add memgraph/skills` |

Then, with Docker running, ask your agent *Get started with Memgraph* to run the `memgraph-start` onboarding (or call it directly: `/memgraph:memgraph-start` in Claude Code, `$memgraph-start` in Codex). In Codex, start it with `codex -a on-request` so the agent can ask to run Docker outside its sandbox. To be asked less, answer the first `docker` and `curl` prompts with **Yes, and don't ask again for commands that start with …**, or choose **Approve for me** in `/permissions`, where Codex's reviewer approves low-risk commands for you.

The Memgraph MCP server runs with `uvx`, so it needs [uv](https://docs.astral.sh/uv/).
It connects to `bolt://localhost:7687` unless you set `MEMGRAPH_URL`.

## Layout

```
.claude-plugin/marketplace.json   Claude Code catalog
.agents/plugins/marketplace.json  Codex catalog
```
