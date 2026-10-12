---
kind: primary
routes:
  web-admin: Web administration
  admin-client: Administration API
steps:
- text: The Administrator invokes revoke recovery link.
  kind: actor
  entities:
  - entity: recovery-link
    effect: reads
    facts: []
  contexts: &id001
    web-admin:
      place: web::administration::users
    admin-client:
      place: client-api::administration
  actor: administrator
- text: The Product deletes the selected outstanding recovery proof.
  kind: product
  entities:
  - entity: recovery-link
    effect: removes
    from: Issued
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
  target: server/db/accountRecovery.ts
---

# Revoke recovery link

## Trigger

The Administrator invokes revoke recovery link.

## Outcome

Outstanding recovery link invalidated
