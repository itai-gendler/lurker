---
appliesTo:
- type: entity
  id: lurker-log
  effect: changes
permits:
- related:
  - verb: has-view
    entity: account
  - verb: has-account
    entity: user
- related:
  - verb: has-view
    entity: account
  - verb: has-account
    entity: administrator
references:
- kind: code
  role: implementation
  target: server/services/systemLog.ts
---

# Lurker log changes require the stated owner or bound entry authority

Own account view of permitted global/private entries; own Read boundary.
