---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes reorder favorites.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::buffers
    client:
      place: client-api::personal
  actor: user
- text: Supplied favorite subset reordered
  kind: product
  entities:
  - entity: favorite-buffer
    effect: changes
    facts:
    - Position
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

# Reorder favorites

## Trigger

The User invokes reorder favorites.

## Outcome

Supplied favorite subset reordered

The supplied favorite subset is reordered while unsupplied entries are retained.
