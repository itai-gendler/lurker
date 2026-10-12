---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes edit highlight rule.
  kind: actor
  entities:
  - entity: highlight-rule
    effect: reads
    facts: []
  contexts: &id001
    web:
      place: web::personal::highlight-rules
    client:
      place: client-api::personal
  actor: user
- text: Editable matching rule changed
  kind: product
  entities:
  - entity: highlight-rule
    effect: changes
    facts:
    - Pattern
    - Mask
    - Matching kind
    - Network scope
    - Channel scope
    - Case sensitivity
    - Enabled
  contexts: *id001
  actor: user
references:
- kind: code
  role: implementation
  target: server/services/highlightRulesService.ts
- kind: code
  role: implementation
  target: server/db/highlightRules.ts
---

# Edit highlight rule

## Trigger

The User invokes edit highlight rule.

## Outcome

Editable matching rule changed
