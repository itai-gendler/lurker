---
kind: exception
routes:
  web: Web
  client: Client API
steps:
- text: The User requests a connection whose subsequent upstream dial or registration fails.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::network
    client:
      place: client-api::personal
  actor: user
- text: Failed upstream connection reported without deleting configuration/history
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

# Connect network connection failed

## Trigger

The User requests a connection whose subsequent upstream dial or registration fails.

## Outcome

Failed upstream connection reported without deleting configuration/history
