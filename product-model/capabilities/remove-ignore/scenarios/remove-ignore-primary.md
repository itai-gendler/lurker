---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes remove ignore.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::ignores
    client:
      place: client-api::personal
  actor: user
- text: Selected matching rules removed
  kind: product
  entities:
  - entity: ignore-rule
    effect: removes
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

# Remove ignore

## Trigger

The User invokes remove ignore.

## Outcome

Selected matching rules removed
