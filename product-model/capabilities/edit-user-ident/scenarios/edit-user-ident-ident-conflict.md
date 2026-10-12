---
kind: exception
routes:
  web-admin: Web administration
  admin-client: Administration API
steps:
- text: "The Administrator assigns an ident colliding case-insensitively with another member identity\u2019\
    s effective ident."
  kind: actor
  entities: []
  contexts: &id001
    web-admin:
      place: web::administration::users
    admin-client:
      place: client-api::administration
  actor: administrator
- text: Conflicting ident assignment refused
  kind: product
  entities: []
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

# Edit user ident ident conflict

## Trigger

The Administrator assigns an ident colliding case-insensitively with another account’s effective ident.

## Outcome

Conflicting ident assignment refused
