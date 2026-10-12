---
entities:
- entity: lurker-log
  shows:
  - Entries
  - Read boundary
  - Unread counts
references:
- kind: code
  role: implementation
  target: vue_client/src/stores/buffers.ts
entryPoints:
- web: /system
---

# Lurker log

Lurker-log entries and read/count facts.
