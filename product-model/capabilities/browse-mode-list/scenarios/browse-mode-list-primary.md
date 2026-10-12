---
kind: primary
routes:
  web: Web
  client: Client API
  irc: IRC bouncer
steps:
- text: The User invokes browse mode list.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::channel
    client:
      place: client-api::personal
    irc:
      place: irc-bouncer::personal
  actor: user
- text: Supported list-mode query result returned
  kind: product
  entities:
  - entity: channel
    effect: reads
    facts:
    - Mode lists
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
  target: server/services/verbs/getModeList.ts
---

# Browse mode list

## Trigger

The User invokes browse mode list.

## Outcome

Supported list-mode query result returned

A live supported list-mode query returns its result, refusal or timeout. The query sends upstream traffic.
