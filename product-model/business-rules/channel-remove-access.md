---
appliesTo:
- type: entity
  id: channel
  effect: removes
permits:
- related:
  - verb: contains
    entity: network
  - verb: owns
    entity: account
  - verb: has-account
    entity: user
- related:
  - verb: contains
    entity: network
  - verb: owns
    entity: account
  - verb: has-account
    entity: administrator
- unattended: true
references:
- kind: code
  role: implementation
  target: server/db/buffers.ts
- kind: code
  role: implementation
  target: server/services/wsHub.ts
---

# Channel removal requires the stated owner or bound entry authority

Create: confirmed/accepted IRC observation or import. Ordinary read: ownership/Agent read/bound B. Mode query: live path and Agent write. Local change: actual read/clear/retention/notification guards. IRC change: join/visibility/autojoin/topic/modes under actual pause/upstream conditions. Remove: eligible collection/parent removal.

Unattended permission is limited to the attributable received event, expiry, delivery-health update or eligible maintenance/parent cleanup described for this operation; it does not authorize arbitrary scheduled account mutation.
