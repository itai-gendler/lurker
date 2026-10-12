---
kind: path
routes:
  web: Web
  client: Client API
steps:
- text: The User adds an ignore specification already matching a saved rule.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::ignores
    client:
      place: client-api::personal
  actor: user
- text: Matching duplicate refreshes lifetime rather than inventing a second independent rule
  kind: product
  entities:
  - entity: ignore-rule
    effect: changes
    facts:
    - Expires at
  contexts: *id001
  actor: user
references:
- kind: code
  role: implementation
  target: server/services/ignoreRulesService.ts
- kind: code
  role: implementation
  target: server/db/ignoredMasks.ts
- kind: code
  role: implementation
  target: server/services/wsHub.ts
---

# Add ignore duplicate lifetime refresh

## Trigger

The User adds an ignore specification already matching a saved rule.

## Outcome

Matching duplicate refreshes lifetime rather than inventing a second independent rule
