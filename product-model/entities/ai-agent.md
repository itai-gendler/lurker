---
kind: system
acts: external
references:
- kind: code
  role: implementation
  target: server/middleware/apiAuth.ts
- kind: code
  role: implementation
  target: server/services/mcpServer.ts
---

# AI agent

An external AI agent acting for an account owner through the presented API token or OAuth delegation.
