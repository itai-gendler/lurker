---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes add network.
  kind: actor
  entities:
  - entity: network
    effect: reads
    facts: []
  contexts: &id001
    web:
      place: web::personal::networks
    client:
      place: client-api::personal
  actor: user
- text: Configuration saved and initial connection requested
  kind: product
  entities:
  - entity: network
    effect: creates
    facts:
    - Name
    - Connection configuration
    - Authentication
    - Connection preferences
    - Startup channels
    - Preferred nick
    - Current nick
    - Connection state
    - Away state
    - CASEMAPPING
    - Listed channels
    - Directory progress
    - Position
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

# Add network

## Trigger

The User invokes add network.

## Outcome

Configuration saved and initial connection requested

The valid name, host and nick configuration is saved and an initial connection is requested. An accepted request does not guarantee completed upstream registration.
