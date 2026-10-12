---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes remove passkey.
  kind: actor
  entities:
  - entity: passkey
    effect: reads
    facts: []
  contexts: &id001
    web:
      place: web::personal::account
    client:
      place: client-api::personal
  actor: user
- text: Owned credential removed while preserving a usable method
  kind: product
  entities:
  - entity: passkey
    effect: removes
    from: Registered
  contexts: *id001
  actor: user
references:
- kind: code
  role: implementation
  target: server/routes/auth.ts
- kind: code
  role: implementation
  target: server/middleware/auth.ts
- kind: code
  role: implementation
  target: server/db/sessions.ts
- kind: code
  role: implementation
  target: server/db/users.ts
---

# Remove passkey

## Trigger

The User invokes remove passkey.

## Outcome

Owned credential removed while preserving a usable method

Removal keeps another usable password or passkey sign-in method.
