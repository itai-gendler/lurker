---
kind: primary
routes:
  application: OAuth application
steps:
- text: The Client application invokes exchange approval.
  kind: actor
  entities: []
  contexts: &id001
    application:
      place: oauth
  actor: client-application
- text: Bound, valid code and PKCE verifier produce access
  kind: product
  entities:
  - entity: authorized-app
    effect: changes
    facts:
    - Issued access
  contexts: *id001
  actor: client-application
references:
- kind: code
  role: implementation
  target: server/routes/oauth.ts
- kind: code
  role: implementation
  target: server/db/oauth.ts#consumeCode
---

# Exchange approval

## Trigger

The Client application invokes exchange approval.

## Outcome

Bound, valid code and PKCE verifier produce access

Exchange consumes the code before later client, return-location and PKCE validation. Success issues OAuth access without an automatic expiry or refresh token.
