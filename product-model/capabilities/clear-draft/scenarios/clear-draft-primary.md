---
kind: primary
routes:
  web: Web
  client: Client API
  web-direct-message: Web direct message
steps:
- text: The User invokes clear draft.
  kind: actor
  entities:
  - entity: draft
    effect: reads
    facts: []
  contexts: &id001
    web:
      place: web::personal::channel
    client:
      place: client-api::personal
    web-direct-message:
      place: web::personal::direct-message
  actor: user
- text: Draft removed and synchronized
  kind: product
  entities:
  - entity: draft
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
  target: server/routes/drafts.ts
- kind: code
  role: implementation
  target: server/db/drafts.ts
---

# Clear draft

## Trigger

The User invokes clear draft.

## Outcome

Draft removed and synchronized
