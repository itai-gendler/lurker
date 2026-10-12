---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes edit network.
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
- text: Supplied owned configuration saved
  kind: product
  entities:
  - entity: network
    effect: changes
    facts:
    - Name
    - Connection configuration
    - Authentication
    - Connection preferences
    - Startup channels
    - Preferred nick
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
---

# Edit network

## Trigger

The User invokes edit network.

## Outcome

Supplied owned configuration saved

Supplied fields are saved. Configuration editing does not imply an immediate reconnect; host changes are checked against policy.
