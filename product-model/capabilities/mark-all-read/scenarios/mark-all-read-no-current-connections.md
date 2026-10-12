---
kind: exception
routes:
  web: Web
  client: Client API
steps:
- text: The User marks all read while the current member identity connection map is empty.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::buffers
    client:
      place: client-api::personal
  actor: user
- text: No current connection objects means no walk updates. Other saved networks and the networkless Lurker
    log retain their prior markers.
  kind: product
  entities:
  - entity: network
    effect: reads
    facts:
    - Connection state
  - entity: lurker-log
    effect: reads
    facts: []
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
  target: server/db/messages.ts
---

# Mark all read no current connections

## Trigger

The User marks all read while the current account connection map is empty.

## Outcome

No current connection objects means no walk updates. Other saved networks and the networkless Lurker log retain their prior markers.
