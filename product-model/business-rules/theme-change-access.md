---
appliesTo:
- type: entity
  id: theme
  effect: changes
permits:
- related:
  - verb: owns
    entity: account
  - verb: has-account
    entity: user
  when:
  - entity: account
    fact: Pause status
    is: Active
- related:
  - verb: owns
    entity: account
  - verb: has-account
    entity: administrator
  when:
  - entity: account
    fact: Pause status
    is: Active
references:
- kind: code
  role: implementation
  target: server/db/themes.ts
- kind: code
  role: implementation
  target: server/services/themesService.ts
---

# Theme changes require the stated owner or bound entry authority

HTTP Owner; saved instances; valid name/value/limit conditions.
