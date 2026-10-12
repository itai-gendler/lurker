---
entities:
- entity: network-log
  shows:
  - Entries
  - Read boundary
  - Clear boundary
  - Unread counts
references:
- kind: code
  role: implementation
  target: server/db/messages.ts
- kind: code
  role: implementation
  target: vue_client/src/stores/buffers.ts
entryPoints:
- web: /buffer/:id
---

# Network log

Network-log entries and read/clear/count facts.
