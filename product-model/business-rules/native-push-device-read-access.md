---
appliesTo:
- type: entity
  id: native-push-device
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
  target: server/db/pushSubscriptions.ts
- kind: code
  role: implementation
  target: server/routes/push.ts
---

# Native push device disclosure requires the stated owner or bound entry authority

Configured supported native registration/rebind; owned disclosure/removal; stored/incoming transport checks; unattended health. Deregistration matches owner+endpoint.
