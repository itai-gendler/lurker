---
appliesTo:
- type: entity
  id: web-push-subscription
  effect: creates
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
  target: server/db/pushSubscriptions.ts
- kind: code
  role: implementation
  target: server/routes/push.ts
---

# Web Push subscription creation requires the stated owner or bound entry authority

Only the authenticated unpaused account registers valid Web Push endpoint/keys. Ordinary cross-owner browser collisions refuse registration; relay-device endpoints require opt-in and the both-WebPush stored/incoming exception.
