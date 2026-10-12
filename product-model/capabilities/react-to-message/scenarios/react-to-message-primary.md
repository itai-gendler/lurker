---
kind: primary
routes:
  web: Web
  client: Client API
  irc: IRC bouncer
  web-direct-message: Web direct message
steps:
- text: The User invokes react to message.
  kind: actor
  entities:
  - entity: message
    effect: reads
    facts: []
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
- text: Eligible upstream reaction becomes recorded
  kind: product
  entities:
  - entity: reaction
    effect: creates
    facts:
    - Value
    - Reacting identity
    - Self attribution
    - Reacted at
    - Removed at
    to: Active
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

# React to message

## Trigger

The User invokes react to message.

## Outcome

Eligible upstream reaction becomes recorded

An eligible recorded upstream message/action receives a supported reaction; incoming reactions and replay follow the same retained identity/timestamp contract.

## Edge cases

- Notice, DCC, missing upstream identity, encrypted channel and missing negotiated eligibility refuse the supported reaction operation.
