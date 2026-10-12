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
  target: server/services/verbs/disconnectNetwork.ts
domain: networks
---

# Disconnect network

Upstream stopped; configuration/history retained.

Stopping the upstream retains saved configuration and history.
