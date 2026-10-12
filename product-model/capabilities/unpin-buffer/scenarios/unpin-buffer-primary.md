---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes unpin buffer.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::buffers
    client:
      place: client-api::personal
  actor: user
- text: Pin removed and order repaired
  kind: product
  entities:
  - entity: pin
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
  target: server/db/pinnedBuffers.ts
---

# Unpin buffer

## Trigger

The User invokes unpin buffer.

## Outcome

Pin removed and order repaired
