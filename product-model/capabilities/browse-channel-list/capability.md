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
---

# Browse channel list

Cached directory searched/browsed.

The cached directory can be searched, filtered and sorted without issuing a fresh upstream LIST.
