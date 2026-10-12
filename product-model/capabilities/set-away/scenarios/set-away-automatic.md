---
kind: path
routes:
  web: Web
  client: Client API
  irc: IRC bouncer
steps:
- text: The established presence or startup condition is observed.
  kind: condition
  entities: []
  contexts: &id001
    web:
      place: web::personal::channel
    client:
      place: client-api::personal
    irc:
      place: irc-bouncer::personal
  unattended: true
- text: Counted absence establishes automatic away after its applicable delay; existing manual away is preserved.
  kind: product
  entities:
  - entity: network
    effect: changes
    facts:
    - Away state
  contexts: *id001
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

# Set away automatic

## Trigger

The Product’s counted presence policy reaches automatic-away eligibility.

## Outcome

Counted absence establishes automatic away after its applicable delay; existing manual away is preserved.
