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
  target: server/services/bouncer.ts
---

# Refresh channel list

Fresh upstream LIST requested; directory progress/results updated.

A fresh LIST requires the live outbound path; directory progress/results update as the upstream replies. Cached browsing remains distinct.
