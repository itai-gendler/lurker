---
kind: exception
routes:
  web: Web
  client: Client API
  irc: IRC bouncer
steps:
- text: The User requests a fresh directory LIST without an available live connection.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::channel-list
    client:
      place: client-api::personal
    irc:
      place: irc-bouncer::personal
  actor: user
- text: Missing live connection prevents a fresh LIST; retained cached data is distinct
  kind: product
  entities:
  - entity: network
    effect: reads
    facts:
    - Connection state
    - Listed channels
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
  target: server/services/bouncer.ts
---

# Refresh channel list offline

## Trigger

The User requests a fresh directory LIST without an available live connection.

## Outcome

Missing live connection prevents a fresh LIST; retained cached data is distinct
