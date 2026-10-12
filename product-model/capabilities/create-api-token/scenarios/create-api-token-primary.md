---
kind: primary
routes:
  web: Web
steps:
- text: The User invokes create api token.
  kind: actor
  entities:
  - entity: api-token
    effect: reads
    facts: []
  contexts: &id001
    web:
      place: web::personal::api-tokens
  actor: user
- text: Scoped token created; raw value revealed once
  kind: product
  entities:
  - entity: api-token
    effect: creates
    facts:
    - Name
    - Scope
    - Created at
    - Last used at
    - Revocation
    to: Active
  contexts: *id001
  actor: user
references:
- kind: code
  role: implementation
  target: server/routes/apiTokens.ts
- kind: code
  role: implementation
  target: server/db/apiTokens.ts
---

# Create api token

## Trigger

The User invokes create api token.

## Outcome

Scoped token created; raw value revealed once

Standalone token creation records read or read-write scope and reveals the raw token only in the creation result.
