---
kind: exception
routes:
  web-admin: Web administration
  admin-client: Administration API
steps:
- text: The Administrator checks relay status and receives an inactive or unavailable subscription result.
  kind: actor
  entities: []
  contexts: &id001
    web-admin:
      place: web::administration::notifications
    admin-client:
      place: client-api::administration
  actor: administrator
- text: Relay check reports inactive/unavailable subscription state
  kind: product
  entities:
  - entity: instance-settings
    effect: changes
    facts:
    - Relay status
  contexts: *id001
  actor: administrator
references:
- kind: code
  role: implementation
  target: server/routes/adminPush.ts
- kind: code
  role: implementation
  target: server/services/push/relayStatus.ts
- kind: code
  role: implementation
  target: server/services/push/relay.ts
---

# Change instance notifications settings inactive relay

## Trigger

The Administrator checks relay status and receives an inactive or unavailable subscription result.

## Outcome

Relay check reports inactive/unavailable subscription state
