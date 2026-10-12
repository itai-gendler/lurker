---
kind: validation
routes:
  web: Web
  client: Client API
steps:
- text: The User tries to remove the only WebAuthn proof when the member identity has no password.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::account
    client:
      place: client-api::personal
  actor: user
- text: Last usable sign-in method cannot be removed
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

# Remove passkey last method

## Trigger

The User tries to remove the only passkey when the account has no password.

## Outcome

Last usable sign-in method cannot be removed
