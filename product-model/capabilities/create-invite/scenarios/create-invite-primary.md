---
kind: primary
routes:
  web-admin: Web administration
  admin-client: Administration API
steps:
- text: The Administrator invokes create invite.
  kind: actor
  entities:
  - entity: invite
    effect: reads
    facts: []
  contexts: &id001
    web-admin:
      place: web::administration::invites
    admin-client:
      place: client-api::administration
  actor: administrator
- text: Expiring invitation issued
  kind: product
  entities:
  - entity: invite
    effect: creates
    facts:
    - Expires at
    - Redeemed at
    - Validity
    to: Available
  contexts: *id001
  actor: administrator
references:
- kind: code
  role: implementation
  target: server/routes/admin.ts
- kind: code
  role: implementation
  target: server/middleware/auth.ts
- kind: code
  role: implementation
  target: server/db/invites.ts
---

# Create invite

## Trigger

The Administrator invokes create invite.

## Outcome

Expiring invitation issued

A positive supported expiry creates an invitation; the default is seven days.
