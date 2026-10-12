---
kind: validation
routes:
  web: Web
  client: Client API
steps:
- text: The User tries to add a configured upstream whose host the current instance policy disallows.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::networks
    client:
      place: client-api::personal
  actor: user
- text: Disallowed host refuses creation/connection
  kind: product
  entities: []
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

# Add network blocked host

## Trigger

The User tries to add a network whose host the current instance policy disallows.

## Outcome

Disallowed host refuses creation/connection
