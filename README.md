# Memgraph plugins for coding agents

Build with [Memgraph](https://memgraph.com) from your coding agent. One install gives
Claude Code or Codex the Memgraph skills, a search over the Memgraph docs, and access
to your Memgraph database.

```
/plugin marketplace add memgraph/marketplace
/plugin install memgraph@memgraph
```

Then, with Docker running, ask your agent:

```
Get started with Memgraph
```

It starts Memgraph and Memgraph Lab in Docker, loads a sample dataset you pick, and runs
a first query and a graph algorithm, in about a minute.

## Plugins

| Plugin | What it adds | Source |
| --- | --- | --- |
| `memgraph` | Skills for Cypher, data modeling, importing data, indexes, configuration, MAGE algorithms, query modules, mgconsole and GraphRAG, plus the `memgraph-start` onboarding. The [Memgraph docs MCP server](https://memgraph.com/docs/getting-started/coding-with-ai/docs-mcp), so the agent looks things up instead of answering from memory. The [Memgraph MCP server](https://memgraph.com/docs/ai-ecosystem/integrations/mcp), so it can read your schema and run queries (read-only by default). | [memgraph/skills](https://github.com/memgraph/skills) |
| `context-graph` | AI Memory: records your agent sessions in Memgraph and recalls them in later sessions. Optional and separate, so nothing is recorded unless you install it. | [memgraph/ai-toolkit](https://github.com/memgraph/ai-toolkit/tree/main/context-graph) |

## Install

### Claude Code

```
/plugin marketplace add memgraph/marketplace
/plugin install memgraph@memgraph
```

### Codex

```bash
codex plugin marketplace add memgraph/marketplace
codex plugin add memgraph@memgraph
```

For the onboarding, start Codex with `codex -a on-request`, so the agent can ask to run
Docker outside its sandbox. To be asked less, answer the first `docker` and `curl`
prompts with **Yes, and don't ask again for commands that start with …**.

### Other agents

```bash
npx skills add memgraph/skills
```

This installs the skills only. To add the docs MCP server, see
[Docs MCP server](https://memgraph.com/docs/getting-started/coding-with-ai/docs-mcp).

### AI Memory

`context-graph` needs the `memgraph-context-graph` CLI. Its installer sets up the CLI,
its own Memgraph and the agent plugins:

```bash
curl -fsSL https://raw.githubusercontent.com/memgraph/ai-toolkit/main/context-graph/scripts/install.sh | bash
```

## Start the onboarding

Ask *Get started with Memgraph*, or call the skill directly: `/memgraph:memgraph-start`
in Claude Code, `$memgraph-start` in Codex. It needs Docker and curl, on macOS or Linux.

## Requirements and settings

- The Memgraph MCP server runs with `uvx`, so it needs [uv](https://docs.astral.sh/uv/).
- It connects to `bolt://localhost:7687`. To use another Memgraph, set `MEMGRAPH_URL`
  (and `MEMGRAPH_USER`, `MEMGRAPH_PASSWORD`, `MEMGRAPH_DATABASE` if needed) before
  you start the agent.
- The docs MCP server (`https://mcp-docs.memgraph.com`) needs no API key or sign-in.

## Updates

A plugin updates when a new version is published.

- **Claude Code:** turn on auto-update for the `memgraph` marketplace in `/plugin`.
- **Codex:** run `codex plugin marketplace upgrade memgraph`, then reinstall with
  `codex plugin remove memgraph@memgraph && codex plugin add memgraph@memgraph`.

## How this repository works

This repository holds only the catalogs. Each plugin lives in the repository where its
code is, so report issues and send changes there.

```
.claude-plugin/marketplace.json   Claude Code catalog
.agents/plugins/marketplace.json  Codex catalog
```

## License

[Apache 2.0](LICENSE)
