---
kind: primary
routes:
  application: OAuth application
steps:
- text: The Client application invokes revoke app token.
  kind: actor
  entities: []
  contexts: &id001
    application:
      place: oauth
  actor: client-application
- text: Matching application token revoked
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
  target: server/db/oauth.ts
---

# Revoke app token

## Trigger

The Client application invokes revoke app token.

## Outcome

Matching application token revoked

The registered client/token association governs revocation; an unknown or unmatched token does not revoke unrelated access.
