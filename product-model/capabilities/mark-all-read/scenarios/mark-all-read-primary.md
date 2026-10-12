---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes mark all read.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::buffers
    client:
      place: client-api::personal
  actor: user
- text: Buffers reached through current connection objects advance to tail
  kind: product
  entities:
  - entity: channel
    effect: changes
    facts:
    - Read boundary
    - Unread counts
  - entity: direct-message
    effect: changes
    facts:
    - Read boundary
    - Unread counts
  - entity: network-log
    effect: changes
    facts:
    - Read boundary
    - Unread counts
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
  target: server/db/messages.ts
---

# Mark all read

## Trigger

The User invokes mark all read.

## Outcome

Buffers reached through current connection objects advance to tail

Only buffers reached by the current IRC-manager connection-map walk advance to retained tails, including closed history reached there. Saved networks outside that map and the networkless Lurker log are unchanged.
