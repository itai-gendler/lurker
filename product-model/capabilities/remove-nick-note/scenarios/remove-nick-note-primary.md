---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes remove nick note.
  kind: actor
  entities:
  - entity: nick-note
    effect: reads
    facts: []
  contexts: &id001
    web:
      place: web::personal::nick-note
    client:
      place: client-api::personal
  actor: user
- text: Private note removed
  kind: product
  entities:
  - entity: nick-note
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
  target: server/services/verbs/setNickNote.ts
---

# Remove nick note

## Trigger

The User invokes remove nick note.

## Outcome

Private note removed
