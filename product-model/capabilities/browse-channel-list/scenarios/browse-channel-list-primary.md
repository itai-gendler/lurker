---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User searches and filters the cached IRC directory.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::channel-list
    client:
      place: client-api::personal
  actor: user
- text: Cached directory searched/browsed
  kind: product
  entities:
  - entity: network
    effect: reads
    facts:
    - Listed channels
    - Directory progress
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

# Browse channel list

## Trigger

The User invokes browse channel list.

## Outcome

Cached directory searched/browsed

The cached directory can be searched, filtered and sorted without issuing a fresh upstream LIST.
