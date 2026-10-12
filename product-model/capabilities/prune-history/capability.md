---
availability:
- place: web::personal
- place: client-api::personal
- place: irc-bouncer::personal
- place: mcp
references:
- kind: code
  role: implementation
  target: server/services/retentionSweeper.ts
- kind: code
  role: implementation
  target: server/services/retentionLimits.ts
- kind: code
  role: implementation
  target: server/db/retention.ts
---

# Prune history

Eligible retained history removed unattended.

Effective account/buffer retention under instance ceilings removes eligible history unattended. Bookmarks and bounded additional reply-thread context remain protected.
