---
kind: primary
routes:
  web-admin: Web administration
  admin-client: Administration API
steps:
- text: The Administrator invokes edit network preset.
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
- text: Offering changed
  kind: product
  entities:
  - entity: network-preset
    effect: changes
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
  actor: administrator
references:
- kind: code
  role: implementation
  target: server/routes/adminNetworks.ts
---

# Edit network preset

## Trigger

The Administrator invokes edit network preset.

## Outcome

Offering changed
