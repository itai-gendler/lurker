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
  target: server/db/pinnedBuffers.ts
---

# Reorder pins

Supplied visible subset reordered.

The supplied visible subset is reordered while remaining hidden entries retain their place; duplicates and unknown entries are normalized in the authoritative response.
