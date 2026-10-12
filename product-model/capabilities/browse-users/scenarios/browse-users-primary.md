---
kind: primary
routes:
  web-admin: Web administration
  admin-client: Administration API
steps:
- text: The Administrator invokes browse users.
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
- text: Administrative roster returned
  kind: product
  entities:
  - entity: account
    effect: reads
    facts:
    - Username
    - Pause status
    - Ident
    - Retained history counts
  - entity: recovery-link
    effect: reads
    facts:
    - Expires at
    - Validity
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

# Browse users

## Trigger

The Administrator invokes browse users.

## Outcome

Administrative roster returned
