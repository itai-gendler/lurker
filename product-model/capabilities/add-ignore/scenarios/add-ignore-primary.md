---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes add ignore.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::ignores
    client:
      place: client-api::personal
  actor: user
- text: Ignore or exception saved
  kind: product
  entities:
  - entity: ignore-rule
    effect: creates
    facts:
    - Mask
    - Pattern
    - Matching kind
    - Network scope
    - Levels
    - Exception status
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

# Add ignore

## Trigger

The User invokes add ignore.

## Outcome

Ignore or exception saved

A valid ignore or exception with owned scope and supported levels is saved. A duplicate specification refreshes its lifetime.

## Edge cases

- Removing or expiring the rule does not rewrite ignore annotations already recorded on older content.
