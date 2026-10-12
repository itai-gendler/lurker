---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes add passkey.
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
- text: Valid cookie-backed ceremony registers a credential
  kind: product
  entities:
  - entity: passkey
    effect: creates
    facts:
    - Label
    - Registration
    - Device information
    - Created at
    - Last used at
    to: Registered
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
- kind: code
  role: implementation
  target: server/services/webauthn.ts
---

# Add passkey

## Trigger

The User invokes add passkey.

## Outcome

Valid cookie-backed ceremony registers a credential

The signed challenge-cookie registration ceremony verifies the credential before saving it.

## Edge cases

- A bearer credential alone cannot finish the challenge-cookie ceremony.
