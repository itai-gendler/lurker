---
appliesTo:
- type: entity
  id: channel
- type: entity
  id: direct-message
- type: entity
  id: bookmark
references:
- kind: code
  role: implementation
  target: server/db/buffers.ts
- kind: code
  role: implementation
  target: server/services/wsHub.ts
- kind: code
  role: implementation
  target: server/db/bookmarks.ts
- kind: code
  role: implementation
  target: server/routes/bookmarks.ts
---

# Closed buffer collection

Old closed conversations are collected only under the actual age/bookmark eligibility. Rechecking reopening prevents deleting a subject that became open during collection. The operation is not equivalent to immediate Close.
