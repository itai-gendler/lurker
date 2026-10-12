---
availability:
- place: web::personal
- place: client-api::personal
- place: irc-bouncer::personal
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
  target: server/db/bufferReads.ts
- kind: code
  role: implementation
  target: server/services/bouncer.ts
---

# Mark read

Shared read pointer advances monotonically.

The accepted shared read pointer advances with MAX semantics. WS accepts a positive finite ID without checking integer, submitted-buffer membership or tail bounds.
