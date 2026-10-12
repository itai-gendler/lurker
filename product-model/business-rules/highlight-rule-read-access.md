---
appliesTo:
- type: entity
  id: highlight-rule
  effect: reads
permits:
- related:
  - verb: owns
    entity: account
  - verb: has-account
    entity: user
- related:
  - verb: owns
    entity: account
  - verb: has-account
    entity: administrator
references:
- kind: code
  role: implementation
  target: server/db/highlightRules.ts
- kind: code
  role: implementation
  target: server/services/highlightRulesService.ts
---

# Highlight rule disclosure requires the stated owner or bound entry authority

HTTP Owner; personal editing/removal only for nonautomatic rules; unattended automatic nick-rule maintenance.
