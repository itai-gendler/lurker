---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes add highlight rule.
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
- text: Valid matching rule saved
  kind: product
  entities:
  - entity: highlight-rule
    effect: creates
    facts:
    - Pattern
    - Mask
    - Matching kind
    - Network scope
    - Channel scope
    - Case sensitivity
    - Enabled
    - Automatic origin
  contexts: *id001
  actor: user
references:
- kind: code
  role: implementation
  target: server/services/highlightRulesService.ts
- kind: code
  role: implementation
  target: server/routes/highlightRules.ts
- kind: code
  role: implementation
  target: server/db/highlightRules.ts
---

# Add highlight rule

## Trigger

The User invokes add highlight rule.

## Outcome

Valid matching rule saved
