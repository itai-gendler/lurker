---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes unfavorite buffer.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::buffers
    client:
      place: client-api::personal
  actor: user
- text: Favorite removed
  kind: product
  entities:
  - entity: favorite-buffer
    effect: removes
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

# Unfavorite buffer

## Trigger

The User invokes unfavorite buffer.

## Outcome

Favorite removed

Removing a favorite does not restore an earlier pin.
