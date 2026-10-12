---
kind: primary
routes:
  web-admin: Web administration
  admin-client: Administration API
steps:
- text: The Administrator invokes remove network preset.
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
- text: Offering removed
  kind: product
  entities:
  - entity: network-preset
    effect: removes
  contexts: *id001
  actor: administrator
references:
- kind: code
  role: implementation
  target: server/routes/adminNetworks.ts
---

# Remove network preset

## Trigger

The Administrator invokes remove network preset.

## Outcome

Offering removed
