---
availability:
- place: web::personal
- place: client-api::personal
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
  target: server/routes/drafts.ts
- kind: code
  role: implementation
  target: server/db/drafts.ts
---

# Save draft

Last-write draft synchronized.

Last-write composition text and optional valid owned reply reference are synchronized to other clients. An existing draft is replaced; empty text without reply clears it.
