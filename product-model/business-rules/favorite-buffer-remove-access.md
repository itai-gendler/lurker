---
appliesTo:
- type: entity
  id: favorite-buffer
  effect: removes
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
- unattended: true
references:
- kind: code
  role: implementation
  target: server/db/favoriteBuffers.ts
- kind: code
  role: implementation
  target: server/services/wsHub.ts
---

# Favorite buffer removal requires the stated owner or bound entry authority

WS-local Owner; owned buffer; supplied reorder membership.

Unattended permission is limited to the attributable received event, expiry, delivery-health update or eligible maintenance/parent cleanup described for this operation; it does not authorize arbitrary scheduled account mutation.
