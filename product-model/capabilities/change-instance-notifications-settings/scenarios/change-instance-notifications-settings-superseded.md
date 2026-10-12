---
kind: exception
routes:
  web-admin: Web administration
  admin-client: Administration API
steps:
- text: The Administrator starts a relay-policy status operation whose result is superseded by a newer policy
    generation.
  kind: actor
  entities: []
  contexts: &id001
    web-admin:
      place: web::administration::notifications
    admin-client:
      place: client-api::administration
  actor: administrator
- text: The stale asynchronous result is discarded so a newer opt-in/status generation is retained.
  kind: product
  entities:
  - entity: instance-settings
    effect: reads
    facts:
    - Relay opt-in
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

# Change instance notifications settings superseded

## Trigger

The Administrator starts a relay-policy status operation whose result is superseded by a newer policy generation.

## Outcome

The stale asynchronous result is discarded so a newer opt-in/status generation is retained.
