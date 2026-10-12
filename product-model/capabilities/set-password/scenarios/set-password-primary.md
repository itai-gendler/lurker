---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes set password.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::account
    client:
      place: client-api::personal
  actor: user
- text: Password established or changed under the applicable current-password guard
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

# Set password

## Trigger

The User invokes set password.

## Outcome

Password established or changed under the applicable current-password guard

The supported password length is 8–256 characters. An existing password requires current-password proof.

## Edge cases

- The account’s existing sessions are not automatically all revoked by an ordinary password change.
