---
kind: path
routes:
  web-public: Web entry
  client-entry: Client entry
steps:
- text: The User answers the signed login challenge with a registered WebAuthn proof.
  kind: actor
  entities: []
  contexts: &id001
    web-public:
      place: web::public::login
    client-entry:
      place: client-api::public
  actor: user
- text: Valid challenge-cookie ceremony signs in
  kind: product
  entities:
  - entity: passkey
    effect: changes
    facts:
    - Last used at
  - entity: session
    effect: creates
    facts:
    - Credential
    - Issued at
    - Expires at
    to: Issued
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

# Sign in passkey

## Trigger

The User answers the signed login challenge with a registered passkey.

## Outcome

Valid challenge-cookie ceremony signs in
