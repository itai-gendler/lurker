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
  target: server/services/ircConnection.ts
- kind: code
  role: implementation
  target: server/services/bouncer.ts
---

# Receive messages

Accepted incoming IRC activity recorded/delivered unattended.

Incoming accepted conversation content is recorded with upstream or receive time and ignore/highlight/reply annotations. App clients receive the recorded representation; bouncer live delivery follows filtered raw IRC relay.
