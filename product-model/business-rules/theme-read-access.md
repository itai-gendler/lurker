---
appliesTo:
- type: entity
  id: theme
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
  target: server/db/themes.ts
- kind: code
  role: implementation
  target: server/services/themesService.ts
---

# Theme disclosure requires the stated owner or bound entry authority

HTTP Owner; saved instances; valid name/value/limit conditions.
