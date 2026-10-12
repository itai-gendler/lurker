---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes remove highlight rule.
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
- text: Editable matching rule removed
  kind: product
  entities:
  - entity: highlight-rule
    effect: removes
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

# Remove highlight rule

## Trigger

The User invokes remove highlight rule.

## Outcome

Editable matching rule removed
