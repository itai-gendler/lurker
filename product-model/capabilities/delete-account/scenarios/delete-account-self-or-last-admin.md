---
kind: validation
routes:
  web-admin: Web administration
  admin-client: Administration API
steps:
- text: "The Administrator requests deletion of the current caller\u2019s own member identity or the only remaining\
    \ administrator."
  kind: actor
  entities: []
  contexts: &id001
    web-admin:
      place: web::administration::users
    admin-client:
      place: client-api::administration
  actor: administrator
- text: Removal returns the established conflict and preserves the protected account and its retained data.
  kind: product
  entities:
  - entity: account
    effect: reads
    facts: []
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

# Delete account self or last admin

## Trigger

The Administrator requests deletion of the current caller’s own account or the only remaining administrator.

## Outcome

Removal returns the established conflict and preserves the protected account and its retained data.
