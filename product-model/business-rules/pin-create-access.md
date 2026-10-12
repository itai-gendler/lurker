---
appliesTo:
- type: entity
  id: pin
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
  target: server/services/wsHub.ts
---

# Pin creation requires the stated owner or bound entry authority

WS-local Owner; owned buffer; supplied reorder membership.
