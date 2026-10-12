---
kind: primary
routes:
  web: Web
  client: Client API
  irc: IRC bouncer
steps:
- text: The User requests a fresh upstream IRC directory.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::channel-list
    client:
      place: client-api::personal
    irc:
      place: irc-bouncer::personal
  actor: user
- text: Fresh upstream LIST requested; directory progress/results updated
  kind: product
  entities:
  - entity: network
    effect: changes
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
- kind: code
  role: implementation
  target: server/services/bouncer.ts
---

# Refresh channel list

## Trigger

The User invokes refresh channel list.

## Outcome

Fresh upstream LIST requested; directory progress/results updated

A fresh LIST requires the live outbound path; directory progress/results update as the upstream replies. Cached browsing remains distinct.
