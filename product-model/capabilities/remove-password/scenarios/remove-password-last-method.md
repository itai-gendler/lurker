---
kind: validation
routes:
  web: Web
  client: Client API
steps:
- text: The User tries to remove the password while no WebAuthn proof is registered.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::account
    client:
      place: client-api::personal
  actor: user
- text: Password removal refused without another method
  kind: product
  entities: []
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

# Remove password last method

## Trigger

The User tries to remove the password while no passkey is registered.

## Outcome

Password removal refused without another method
