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
- kind: code
  role: implementation
  target: server/db/messages.ts
---

# Mark all read

Buffers reached through current connection objects advance to tail.

Only buffers reached by the current IRC-manager connection-map walk advance to retained tails, including closed history reached there. Saved networks outside that map and the networkless Lurker log are unchanged.
