---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes disconnect network.
  kind: actor
  entities:
  - entity: network
    effect: reads
    facts: []
  contexts: &id001
    web:
      place: web::personal::network
    client:
      place: client-api::personal
  actor: user
- text: Upstream stopped; configuration/history retained
  kind: product
  entities:
  - entity: network
    effect: changes
    facts:
    - Connection state
  contexts: *id001
  actor: user
references:
- kind: code
  role: implementation
  target: server/routes/networks.ts
- kind: code
  role: implementation
  target: server/db/networks.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
- kind: code
  role: implementation
  target: server/services/verbs/disconnectNetwork.ts
---

# Disconnect network

## Trigger

The User invokes disconnect network.

## Outcome

Upstream stopped; configuration/history retained

Stopping the upstream retains saved configuration and history.
