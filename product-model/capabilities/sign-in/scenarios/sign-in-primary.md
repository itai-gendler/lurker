---
kind: primary
routes:
  web-public: Web entry
  client-entry: Client entry
steps:
- text: The User invokes sign in.
  kind: actor
  entities: []
  contexts: &id001
    web-public:
      place: web::public::login
    client-entry:
      place: client-api::public
  actor: user
- text: Valid supported credential issues an account session
  kind: product
  entities:
  - entity: account
    effect: reads
    facts:
    - Username
    - Sign-in methods
    - Pause status
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

# Sign in

## Trigger

The User invokes sign in.

## Outcome

Valid supported credential issues an account session

Supported password sign-in issues a fixed-lifetime ordinary session. Web uses its cookie; the client password-token endpoint returns a bearer session. Passkey sign-in uses the challenge-cookie ceremony.

## Edge cases

- Paused accounts retain permitted read access but have operation-specific write restrictions. Invalid proofs and current backoff refuse sign-in.
