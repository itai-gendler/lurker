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
- text: Applicable automatic away clears when counted presence returns. This does not indiscriminately clear
    manual away.
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

# Clear away presence return

## Trigger

The Product observes counted presence return while the applicable away state was set automatically.

## Outcome

Applicable automatic away clears when counted presence returns. This does not indiscriminately clear manual away.
