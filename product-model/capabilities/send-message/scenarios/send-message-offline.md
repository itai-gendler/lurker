---
kind: exception
routes:
  web: Web
  client: Client API
  irc: IRC bouncer
  web-direct-message: Web direct message
steps:
- text: The User submits conversation content while the applicable upstream send path is unavailable.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::channel
    client:
      place: client-api::personal
    irc:
      place: irc-bouncer::personal
    web-direct-message:
      place: web::personal::direct-message
  actor: user
- text: Unavailable connection prevents outbound send
  kind: product
  entities: []
  contexts: *id001
  actor: user
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
  target: server/services/verbs/sendMessage.ts
- kind: code
  role: implementation
  target: server/services/verbs/sendAction.ts
- kind: code
  role: implementation
  target: server/services/verbs/sendNotice.ts
- kind: code
  role: implementation
  target: server/services/bouncer.ts
---

# Send message offline

## Trigger

The User submits conversation content while the applicable upstream send path is unavailable.

## Outcome

Unavailable connection prevents outbound send
