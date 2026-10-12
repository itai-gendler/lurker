---
kind: exception
routes:
  web: Web
  client: Client API
  web-direct-message: Web direct message
steps:
- text: The User saves unsent composition text with an invalid or unavailable reply reference.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::channel
    client:
      place: client-api::personal
    web-direct-message:
      place: web::personal::direct-message
  actor: user
- text: Invalid reply reference dropped while draft text is retained as supported
  kind: product
  entities:
  - entity: draft
    effect: changes
    facts:
    - Text
    - Reply reference
    - Updated at
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
  target: server/routes/drafts.ts
- kind: code
  role: implementation
  target: server/db/drafts.ts
---

# Save draft invalid reply dropped

## Trigger

The User saves draft text with an invalid or unavailable reply reference.

## Outcome

Invalid reply reference dropped while draft text is retained as supported
