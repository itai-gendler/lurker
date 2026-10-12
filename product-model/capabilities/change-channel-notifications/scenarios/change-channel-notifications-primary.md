---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes change channel notifications.
  kind: actor
  entities:
  - entity: channel
    effect: reads
    facts: []
  contexts: &id001
    web:
      place: web::personal::channel
    client:
      place: client-api::personal
  actor: user
- text: Channel notification override changes
  kind: product
  entities:
  - entity: channel
    effect: changes
    facts:
    - Notification override
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
---

# Change channel notifications

## Trigger

The User invokes change channel notifications.

## Outcome

Channel notification override changes
