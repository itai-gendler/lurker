---
kind: primary
routes:
  web-admin: Web administration
  admin-client: Administration API
steps:
- text: The Administrator invokes resume account.
  kind: actor
  entities:
  - entity: account
    effect: reads
    facts: []
  contexts: &id001
    web-admin:
      place: web::administration::users
    admin-client:
      place: client-api::administration
  actor: administrator
- text: Pause cleared; configured connections initialized
  kind: product
  entities:
  - entity: account
    effect: changes
    facts:
    - Pause status
    to: Active
    from: Paused
  - entity: network
    effect: changes
    facts:
    - Connection state
  contexts: *id001
  actor: administrator
references:
- kind: code
  role: implementation
  target: server/routes/admin.ts
- kind: code
  role: implementation
  target: server/middleware/auth.ts
---

# Resume account

## Trigger

The Administrator invokes resume account.

## Outcome

Pause cleared; configured connections initialized

Standalone resume clears pause and initializes configured connections; confirmed registration remains asynchronous.
