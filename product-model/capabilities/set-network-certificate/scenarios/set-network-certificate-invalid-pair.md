---
kind: validation
routes:
  web: Web
  client: Client API
steps:
- text: The User submits an invalid certificate or private-key pair.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::network
    client:
      place: client-api::personal
  actor: user
- text: Invalid certificate/private-key input refused
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

# Set network certificate invalid pair

## Trigger

The User submits an invalid certificate or private-key pair.

## Outcome

Invalid certificate/private-key input refused
