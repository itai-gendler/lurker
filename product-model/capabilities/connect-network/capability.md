---
availability:
- place: web::personal
- place: client-api::personal
- place: mcp
references:
- kind: code
  role: implementation
  target: server/routes/networks.ts
- kind: code
  role: implementation
  target: server/db/networks.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
- kind: code
  role: implementation
  target: server/services/verbs/connectNetwork.ts
domain: networks
---

# Connect network

Connection start requested; subsequent upstream state is separate.

The host/proxy policy and account state are checked before requesting a dial. Reconnect replaces the prior connection; MCP force:true is its reconnect path.
