---
kind: primary
routes:
  web: Web
steps:
- text: The User invokes revoke api token.
  kind: actor
  entities:
  - entity: api-token
    effect: reads
    facts: []
  contexts: &id001
    web:
      place: web::personal::api-tokens
  actor: user
- text: Token revoked; associated IRC attachments closed
  kind: product
  entities:
  - entity: api-token
    effect: changes
    facts:
    - Revocation
    to: Revoked
    from: Active
  - entity: irc-client
    effect: removes
    from: Attached
  contexts: *id001
  actor: user
references:
- kind: code
  role: implementation
  target: server/routes/apiTokens.ts
- kind: code
  role: implementation
  target: server/db/apiTokens.ts
- kind: code
  role: implementation
  target: server/services/bouncer.ts
---

# Revoke api token

## Trigger

The User invokes revoke api token.

## Outcome

Token revoked; associated IRC attachments closed
