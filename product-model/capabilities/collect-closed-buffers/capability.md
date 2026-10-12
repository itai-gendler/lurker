---
availability:
- place: web::personal
- place: client-api::personal
- place: irc-bouncer::personal
references:
- kind: code
  role: implementation
  target: server/services/retentionSweeper.ts
- kind: code
  role: implementation
  target: server/db/buffers.ts
---

# Collect closed buffers

Eligible closed subjects removed unattended.

Only otherwise eligible old closed subjects are collected unattended; bookmarks and a reopening guard can preserve them.
