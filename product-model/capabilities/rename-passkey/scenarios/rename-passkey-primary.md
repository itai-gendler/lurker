---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes rename passkey.
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
- text: Owned passkey label changes
  kind: product
  entities:
  - entity: passkey
    effect: changes
    facts:
    - Label
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

# Rename passkey

## Trigger

The User invokes rename passkey.

## Outcome

Owned passkey label changes
