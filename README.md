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

MemCell provides persistent, adaptive cognitive memory for AI agents across any client harness. This repository contains the official MCP registry manifest, Smithery configuration, and connection guides.

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

### Option C: Air-Gapped Local Server (PGlite)

Run MemCell entirely offline on your local machine with embedded PGlite vector storage:

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

MemCell exposes three core cognitive memory tools over MCP:

1. **`recall`**: Pre-flight memory retrieval before taking action. Fetches relevant memories, established principles, and active operational scopes.
2. **`remember`**: Durable memory storage. Files atomic facts, directives, and observations directly into the active workspace.
3. **`report`**: Outcome feedback calibration. Reports whether recalled memory worked, failed, or was avoided, calibrating confidence dynamically over time.

---

## Ecosystem

- **DevKit**: TypeScript SDK, Python SDK, and CLI in [memcell-ai/devkit](https://github.com/memcell-ai/devkit)
- **Engine**: Core memory service backend in [memcell-ai/memcell](https://github.com/memcell-ai/memcell)
- **Documentation**: [memcell.ai/docs](https://memcell.ai/docs)

## License

Apache-2.0
