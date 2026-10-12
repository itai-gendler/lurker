---
availability:
- place: web::personal
- place: client-api::personal
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
  target: server/services/verbs/setRelayBot.ts
---

# Mark relay bot

Nick/template mark saved.

The network/nick envelope mark is saved or replaced. Supported templates unwrap display attribution with bounded nesting while retaining original content.
