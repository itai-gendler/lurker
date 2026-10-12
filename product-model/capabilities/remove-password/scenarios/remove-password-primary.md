---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes remove password.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::account
    client:
      place: client-api::personal
  actor: user
- text: Password sign-in removed while another method remains
  kind: product
  entities:
  - entity: account
    effect: changes
    facts:
    - Sign-in methods
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

# Remove password

## Trigger

The User invokes remove password.

## Outcome

Password sign-in removed while another method remains

Password removal keeps a registered passkey as another usable method.
