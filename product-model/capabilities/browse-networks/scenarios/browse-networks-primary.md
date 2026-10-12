---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes browse networks.
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
- text: Surface-specific owned network information returned
  kind: product
  entities:
  - entity: network
    effect: reads
    facts:
    - Name
    - Current nick
    - Connection state
    - Connection configuration
    - Connection preferences
  - entity: network-preset
    effect: reads
    facts:
    - Name
    - Host
    - Port
    - TLS
    - Recommended channels
    - Authentication guidance
    - Enabled
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

# Browse networks

## Trigger

The User invokes browse networks.

## Outcome

Surface-specific owned network information returned

Personal clients receive owned configuration/state. Bouncer control mode exposes its account’s selectable networks; MCP returns its registered projection.
