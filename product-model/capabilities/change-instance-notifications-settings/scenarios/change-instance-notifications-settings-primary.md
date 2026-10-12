---
kind: primary
routes:
  web-admin: Web administration
  admin-client: Administration API
steps:
- text: The Administrator invokes change instance notifications settings.
  kind: actor
  entities: []
  contexts: &id001
    web-admin:
      place: web::administration::notifications
    admin-client:
      place: client-api::administration
  actor: administrator
- text: Relay policy/status process completes
  kind: product
  entities:
  - entity: instance-settings
    effect: changes
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

# Change instance notifications settings

## Trigger

The Administrator invokes change instance notifications settings.

## Outcome

Relay policy/status process completes

Relay opt-in and explicit status checking use their supported administrative paths. An explicit check may contact the relay while delivery is disabled; superseded asynchronous results cannot overwrite newer policy.
