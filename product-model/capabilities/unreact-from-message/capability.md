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
  target: server/db/reactions.ts
- kind: code
  role: implementation
  target: server/services/bouncer.ts
---

# Unreact from message

Eligible reaction withdrawn with tombstone.

Withdrawal retains a MAX-timestamp tombstone rather than deleting independently; stale replay cannot revive it.
