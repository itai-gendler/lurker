---
appliesTo:
- type: entity
  id: web-push-subscription
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

# Web Push subscription disclosure requires the stated owner or bound entry authority

HTTP Owner; ordinary browser cross-owner collision refused; both-WebPush relay-device rebind exception; relay policy gate; owned heartbeat/removal and unattended health.
