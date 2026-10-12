---
kind: validation
routes:
  web-admin: Web administration
  admin-client: Administration API
steps:
- text: "The Administrator requests pause of the current caller\u2019s own member identity."
  kind: actor
  entities: []
  contexts: &id001
    web-admin:
      place: web::administration::users
    admin-client:
      place: client-api::administration
  actor: administrator
- text: Administrator cannot pause their own account
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

# Pause account self refused

## Trigger

The Administrator requests pause of the current caller’s own account.

## Outcome

Administrator cannot pause their own account
