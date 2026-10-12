---
kind: exception
routes:
  web: Web
  client: Client API
  irc: IRC bouncer
steps:
- text: Incoming IRC activity or available engine backlog arrives.
  kind: condition
  entities: []
  contexts: &id001
    web:
      place: web::personal::channel
    client:
      place: client-api::personal
    irc:
      place: irc-bouncer::personal
  unattended: true
- text: The continuity gap is surfaced in network output. Missing history is not fabricated and lossless recovery
    is not promised.
  kind: product
  entities:
  - entity: network
    effect: reads
    facts:
    - Connection state
  contexts: *id001
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

# Receive messages engine gap

## Trigger

The Product adopts an upstream connection whose engine continuity report contains a gap.

## Outcome

The continuity gap is surfaced in network output. Missing history is not fabricated and lossless recovery is not promised.
