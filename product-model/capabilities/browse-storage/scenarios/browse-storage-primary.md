---
kind: primary
routes:
  web-admin: Web administration
  admin-client: Administration API
steps:
- text: The Administrator invokes browse storage.
  kind: actor
  entities: []
  contexts: &id001
    web-admin:
      place: web::administration::storage
    admin-client:
      place: client-api::administration
  actor: administrator
- text: Storage attribution and ceilings returned
  kind: product
  entities:
  - entity: instance-settings
    effect: reads
    facts:
    - Storage measurements
    - Retention ceilings
  - entity: account
    effect: reads
    facts:
    - Username
    - Retained history counts
  contexts: *id001
  actor: administrator
references:
- kind: code
  role: implementation
  target: server/routes/adminStorage.ts
---

# Browse storage

## Trigger

The Administrator invokes browse storage.

## Outcome

Storage attribution and ceilings returned
