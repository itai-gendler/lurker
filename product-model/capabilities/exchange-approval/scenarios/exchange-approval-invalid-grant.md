---
kind: validation
routes:
  application: OAuth application
steps:
- text: The Client application presents a code with an invalid client, return location, expiry or verifier.
  kind: actor
  entities: []
  contexts: &id001
    application:
      place: oauth
  actor: client-application
- text: The exchange returns invalid_grant. A code found for exchange is consumed before later binding/verifier
    checks and cannot be retried after those failures.
  kind: product
  entities: []
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

# Exchange approval invalid grant

## Trigger

The Client application presents a code with an invalid client, return location, expiry or verifier.

## Outcome

The exchange returns invalid_grant. A code found for exchange is consumed before later binding/verifier checks and cannot be retried after those failures.
