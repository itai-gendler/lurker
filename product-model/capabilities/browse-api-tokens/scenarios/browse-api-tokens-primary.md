---
kind: primary
routes:
  web: Web
steps:
- text: The User invokes browse api tokens.
  kind: actor
  entities:
  - entity: api-token
    effect: reads
    facts: []
  contexts: &id001
    web:
      place: web::personal::api-tokens
  actor: user
- text: Owned token metadata displayed
  kind: product
  entities:
  - entity: api-token
    effect: reads
    facts:
    - Name
    - Scope
    - Created at
    - Last used at
    - Revocation
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

# Browse api tokens

## Trigger

The User invokes browse api tokens.

## Outcome

Owned token metadata displayed
