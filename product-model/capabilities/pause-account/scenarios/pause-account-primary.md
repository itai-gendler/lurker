---
kind: primary
routes:
  web-admin: Web administration
  admin-client: Administration API
steps:
- text: The Administrator invokes pause account.
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
- text: Target paused; live IRC/bouncer access stopped
  kind: product
  entities:
  - entity: account
    effect: changes
    facts:
    - Pause status
    to: Paused
    from: Active
  - entity: network
    effect: changes
    facts:
    - Connection state
  - entity: irc-client
    effect: removes
    from: Attached
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

# Pause account

## Trigger

The Administrator invokes pause account.

## Outcome

Target paused; live IRC/bouncer access stopped

Standalone pause stops target IRC/bouncer access and retains data. Existing WebSocket connections can remain under their exact operation guards.
