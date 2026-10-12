---
appliesTo:
- type: entity
  id: native-push-device
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

# Native push device creation requires the stated owner or bound entry authority

Only the authenticated unpaused account registers a valid token for an actually configured APNs/FCM sender. Cross-owner rebinding requires both stored and incoming transports to be native; mixed collisions refuse.
