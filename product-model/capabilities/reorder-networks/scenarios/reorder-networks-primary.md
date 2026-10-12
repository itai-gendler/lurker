---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes reorder networks.
  kind: actor
  entities:
  - entity: network
    effect: reads
    facts: []
  contexts: &id001
    web:
      place: web::personal::networks
    client:
      place: client-api::personal
  actor: user
- text: Owned network order changes
  kind: product
  entities:
  - entity: network
    effect: changes
    facts:
    - Position
  contexts: *id001
  actor: user
references:
- kind: code
  role: implementation
  target: server/routes/networks.ts
- kind: code
  role: implementation
  target: server/db/networks.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
---

# Reorder networks

## Trigger

The User invokes reorder networks.

## Outcome

Owned network order changes

The valid owned network order is persisted and returned.

## Edge cases

- Missing array returns 400; a current-set length or valid-ID mismatch returns 409 with the authoritative roster before writes.
- Duplicate IDs are not separately rejected and can leave an omitted row’s prior position unchanged.
