---
type: agent
actors:
- ai-agent
references:
- kind: code
  role: implementation
  target: server/app.ts
- kind: code
  role: implementation
  target: server/services/mcpServer.ts
entryPoints:
- agent: /mcp
---

# MCP

The stateless authenticated MCP HTTP contract exposes registered tools to an AI agent acting for an account owner. It has no asynchronous subscription stream.
