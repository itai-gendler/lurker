---
kind: validation
routes:
  web-public: Web entry
  client-entry: Client entry
steps:
- text: The User submits an invalid password or WebAuthn proof login proof.
  kind: actor
  entities: []
  contexts: &id001
    web-public:
      place: web::public::login
    client-entry:
      place: client-api::public
  actor: user
- text: Invalid credentials refused
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

# Sign in invalid credential

## Trigger

The User submits an invalid password or passkey login proof.

## Outcome

Invalid credentials refused
