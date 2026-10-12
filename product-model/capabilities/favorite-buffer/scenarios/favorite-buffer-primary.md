---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes favorite buffer.
  kind: actor
  entities:
  - entity: favorite-buffer
    effect: reads
    facts: []
  contexts: &id001
    web:
      place: web::personal::buffers
    client:
      place: client-api::personal
  actor: user
- text: Cross-network favorite added
  kind: product
  entities:
  - entity: favorite-buffer
    effect: creates
    facts:
    - Position
  - entity: pin
    effect: removes
  - entity: network
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
  target: server/db/favoriteBuffers.ts
---

# Favorite buffer

## Trigger

The User invokes favorite buffer.

## Outcome

Cross-network favorite added

Favoriting adds cross-network organization and removes an existing pin.
