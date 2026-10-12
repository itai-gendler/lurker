---
availability:
- place: web::personal
- place: client-api::personal
- place: irc-bouncer::personal
- place: mcp
references:
- kind: code
  role: implementation
  target: server/services/wsHub.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
- kind: code
  role: implementation
  target: server/db/buffers.ts
- kind: code
  role: implementation
  target: vue_client/src/stores/buffers.ts
- kind: code
  role: implementation
  target: server/services/verbs/setNick.ts
---

# Change nick

Nick change requested; upstream outcome reported where supported.

A nick change is requested and observed upstream nick state is updated when reported.
