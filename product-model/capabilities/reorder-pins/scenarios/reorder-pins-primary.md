---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes reorder pins.
  kind: actor
  entities:
  - entity: pin
    effect: reads
    facts: []
  contexts: &id001
    web:
      place: web::personal::buffers
    client:
      place: client-api::personal
  actor: user
- text: Supplied visible subset reordered
  kind: product
  entities:
  - entity: pin
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
  target: server/db/pinnedBuffers.ts
---

# Reorder pins

## Trigger

The User invokes reorder pins.

## Outcome

Supplied visible subset reordered

The supplied visible subset is reordered while remaining hidden entries retain their place; duplicates and unknown entries are normalized in the authoritative response.
