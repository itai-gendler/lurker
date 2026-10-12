---
kind: exception
routes:
  web: Web
  client: Client API
steps:
- text: The User requests replacement of a connection whose fresh upstream dial fails.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::network
    client:
      place: client-api::personal
  actor: user
- text: Replacement dial fails; asynchronous state reported
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
  target: server/services/verbs/connectNetwork.ts
---

# Reconnect network connection failed

## Trigger

The User requests replacement of a connection whose fresh upstream dial fails.

## Outcome

Replacement dial fails; asynchronous state reported
