---
appliesTo:
- type: entity
  id: favorite-buffer
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
  target: server/db/favoriteBuffers.ts
- kind: code
  role: implementation
  target: server/services/wsHub.ts
---

# Favorite buffer creation requires the stated owner or bound entry authority

WS-local Owner; owned buffer; supplied reorder membership.
