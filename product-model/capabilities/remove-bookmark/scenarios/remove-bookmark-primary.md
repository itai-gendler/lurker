---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes remove bookmark.
  kind: actor
  entities:
  - entity: bookmark
    effect: reads
    facts: []
  contexts: &id001
    web:
      place: web::personal::bookmarks
    client:
      place: client-api::personal
  actor: user
- text: Saved association removed
  kind: product
  entities:
  - entity: bookmark
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
  target: server/routes/bookmarks.ts
- kind: code
  role: implementation
  target: server/db/bookmarks.ts
---

# Remove bookmark

## Trigger

The User invokes remove bookmark.

## Outcome

Saved association removed
