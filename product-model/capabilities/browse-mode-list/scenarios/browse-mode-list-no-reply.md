---
kind: exception
routes:
  web: Web
  client: Client API
  irc: IRC bouncer
steps:
- text: The User requests a live mode list for which no complete reply arrives before timeout.
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
- text: Query timeout/no reply completes without fabricated list success
  kind: product
  entities: []
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

# Browse mode list no reply

## Trigger

The User requests a live mode list for which no complete reply arrives before timeout.

## Outcome

Query timeout/no reply completes without fabricated list success
