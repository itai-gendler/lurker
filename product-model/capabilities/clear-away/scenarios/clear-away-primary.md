---
kind: primary
routes:
  web: Web
  client: Client API
  irc: IRC bouncer
steps:
- text: The User invokes clear away.
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
- text: Applicable away state cleared
  kind: product
  entities:
  - entity: network
    effect: changes
    facts:
    - Away state
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
  target: server/services/verbs/setAway.ts
---

# Clear away

## Trigger

The User invokes clear away.

## Outcome

Applicable away state cleared

Manual away/back uses the applicable network scope. Automatic away is separately triggered by counted presence and never overwrites manual away.
