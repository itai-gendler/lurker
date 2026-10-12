---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes pin buffer.
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
- text: Per-network pin added
  kind: product
  entities:
  - entity: pin
    effect: creates
    facts:
    - Position
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
  target: server/db/pinnedBuffers.ts
---

# Pin buffer

## Trigger

The User invokes pin buffer.

## Outcome

Per-network pin added
