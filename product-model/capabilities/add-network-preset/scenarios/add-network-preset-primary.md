---
kind: primary
routes:
  web-admin: Web administration
  admin-client: Administration API
steps:
- text: The Administrator invokes add network preset.
  kind: actor
  entities:
  - entity: network-preset
    effect: reads
    facts: []
  contexts: &id001
    web-admin:
      place: web::administration::networks
    admin-client:
      place: client-api::administration
  actor: administrator
- text: Offered network configuration saved
  kind: product
  entities:
  - entity: network-preset
    effect: creates
    facts:
    - Name
    - Host
    - Port
    - TLS
    - Recommended channels
    - Authentication guidance
    - Enabled
    - Position
  - entity: network
    effect: reads
    facts: []
  contexts: *id001
  actor: administrator
references:
- kind: code
  role: implementation
  target: server/routes/adminNetworks.ts
---

# Add network preset

## Trigger

The Administrator invokes add network preset.

## Outcome

Offered network configuration saved
