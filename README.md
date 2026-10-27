<p align="center">
  <img src="https://memcell.ai/icon.svg" width="56" alt="MemCell Logo" />
</p>

<h1 align="center">MemCell MCP Server</h1>

<p align="center">
  <strong>The official Model Context Protocol (MCP) server & registry manifest for <a href="https://memcell.ai">MemCell</a>.</strong><br />
  Living, persistent memory for AI agents: recall before acting, report outcomes so confidence is earned.
</p>

<p align="center">
  <a href="https://github.com/memcell-ai/mcp/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-Apache--2.0-blue.svg" alt="License: Apache-2.0" /></a>
  <a href="https://memcell.ai/docs"><img src="https://img.shields.io/badge/docs-memcell.ai-blue" alt="Documentation" /></a>
  <a href="https://smithery.ai/server/@memcell/mcp"><img src="https://smithery.ai/badge/@memcell/mcp" alt="Smithery" /></a>
</p>

MemCell provides persistent, adaptive memory, working thread continuity, knowledge graph traversal, and grounded document RAG for AI agents across any client harness. This repository contains the official MCP registry manifest, Smithery configuration, and connection guides.

---

## Quickstart

### Option A: Local stdio (Recommended)

Run via `npx` (requires `memcell` CLI installed or accessible via npm):

```bash
npx -y memcell mcp
```

### Option B: Remote Streamable HTTP

Connect directly to the hosted or self-hosted MemCell streamable HTTP endpoint:

- **Endpoint**: `https://memcell.ai/mcp`
- **Header**: `Authorization: Bearer <agent-key>`

### Option C: Local Standalone Server (PGlite)

Run MemCell on your local machine with embedded PGlite vector storage (once cached or pointed at `MEMCELL_SERVER_PATH`, `memcell start` runs completely offline without network access):

```bash
# 1. Start local server in background
memcell start --daemon

# 2. Wire local MCP tools
memcell connect --url http://localhost:3000
```

---

## Client Configurations

### 1. Claude Desktop

Add to `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "memcell": {
      "command": "npx",
      "args": ["-y", "memcell", "mcp"]
    }
  }
}
```

### 2. Claude Code

Run:

```bash
claude mcp add memcell -- npx -y memcell mcp
```

### 3. Cursor

Add to `.cursor/mcp.json` (or `~/.cursor/mcp.json`):

```json
{
  "mcpServers": {
    "memcell": {
      "command": "npx",
      "args": ["-y", "memcell", "mcp"]
    }
  }
}
```

### 4. Antigravity

Add to `~/.gemini/antigravity/mcp_config.json`:

```json
{
  "mcpServers": {
    "memcell": {
      "command": "npx",
      "args": ["-y", "memcell", "mcp"]
    }
  }
}
```

### 5. Windsurf / Cline / OpenCode / Goose

Configure the MCP server command as:
- **Command**: `npx`
- **Args**: `["-y", "memcell", "mcp"]`

---

## How It Works

MemCell exposes seven workspace tools over MCP:

1. **`recall`**: Pre-flight memory retrieval before taking action. Fetches relevant instructions, decisions, facts, preferences, active or resumed session threads, 1-hop knowledge graph relations, and grounded workspace document chunks.
2. **`remember`**: Durable memory storage. Files atomic instructions, decisions, facts, and preferences—including detailed operational specifications (`content`), affected resources (`resources`), and enforcement moments (`appliesAt`)—directly into the active workspace or user profile.
3. **`report`**: Outcome feedback calibration. Reports whether recalled memory worked, failed, or was avoided, calibrating confidence dynamically over time.
4. **`feedback`**: Direct evaluation of a specific memory ID (`worked` or `failed`) with supporting outcome notes.
5. **`ingest_document`**: Multi-format document ingestion. Indexes PDF, DOCX, CSV, TSV, HTML, JSON, and Markdown documents into grounded workspace chunks and optionally distills atomic memories.
6. **`search_documents`**: Hybrid semantic and full-text retrieval across grounded workspace document chunks.
7. **`get_insights`**: Live workspace telemetry, empirical Confidence Calibration Curve (`ECE`, Brier score, and bucketed observed success rates), and Governance Shield metrics (enforced guards, quarantined user-scope memories, and demoted items).

---

## Custom Agent SDK Integrations

Building custom agents in TypeScript or Python? Official drop-in adapters ship inside `@memcell/sdk` (`@memcell/sdk/vercel`, `@memcell/sdk/openai`, `@memcell/sdk/langgraph`) and Python `memcell.integrations` (OpenAI Agents, LangGraph, PydanticAI, CrewAI) alongside MCP.

---

## Ecosystem

- **DevKit**: TypeScript SDK, Python SDK, and CLI in [memcell-ai/devkit](https://github.com/memcell-ai/devkit)
- **Engine**: Core memory service backend in [memcell-ai/memcell](https://github.com/memcell-ai/memcell)
- **Documentation**: [memcell.ai/docs](https://memcell.ai/docs)

## License

Apache-2.0
