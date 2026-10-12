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
  target: server/services/verbs/getNickNote.ts
---

# Read nick note

Owned network-scoped private note returned.
