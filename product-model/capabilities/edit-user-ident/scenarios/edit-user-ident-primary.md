---
kind: primary
routes:
  web-admin: Web administration
  admin-client: Administration API
steps:
- text: The Administrator invokes edit user ident.
  kind: actor
  entities:
  - entity: user
    effect: reads
    facts: []
  contexts: &id001
    web-admin:
      place: web::administration::users
    admin-client:
      place: client-api::administration
  actor: administrator
- text: Ident override assigned or cleared
  kind: product
  entities:
  - entity: account
    effect: changes
    facts:
    - Ident
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

# Edit user ident

## Trigger

The Administrator invokes edit user ident.

## Outcome

Ident override assigned or cleared

Standalone ident assignment validates format and effective uniqueness. Clearing returns to the effective default. Changes apply on a subsequent connection, without an automatic reconnect.
