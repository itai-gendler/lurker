---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User saves the selected retained item.
  kind: actor
  entities:
  - entity: message
    effect: reads
    facts: []
  contexts: &id001
    web:
      place: web::personal::channel
    client:
      place: client-api::personal
  actor: user
- text: Owned message association saved
  kind: product
  entities:
  - entity: bookmark
    effect: creates
    facts:
    - Saved at
  - entity: message
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
  target: server/routes/bookmarks.ts
- kind: code
  role: implementation
  target: server/db/bookmarks.ts
---

# Bookmark message

## Trigger

The User invokes bookmark message.

## Outcome

Owned message association saved
