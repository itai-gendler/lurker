---
appliesTo:
- type: entity
  id: ignore-rule
  effect: creates
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
  target: server/db/ignoredMasks.ts
- kind: code
  role: implementation
  target: server/services/ignoreRulesService.ts
---

# Ignore rule creation requires the stated owner or bound entry authority

Owner through actual HTTP/WS guards, valid matching/scope fields; duplicate refresh and unattended expiry.
