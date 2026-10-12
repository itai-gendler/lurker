---
kind: exception
routes:
  web: Web
  client: Client API
  irc: IRC bouncer
  web-direct-message: Web direct message
steps:
- text: The User tries a emoji response without the required upstream retained line eligibility or negotiated support.
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
- text: Missing upstream eligibility/capability refuses reaction
  kind: product
  entities:
  - entity: reaction
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
  target: server/db/reactions.ts
- kind: code
  role: implementation
  target: server/services/bouncer.ts
---

# React to message unsupported

## Trigger

The User tries a reaction without the required upstream message eligibility or negotiated support.

## Outcome

Missing upstream eligibility/capability refuses reaction
