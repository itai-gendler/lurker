---
appliesTo:
- type: entity
  id: network-log
  effect: changes
permits:
- related:
  - verb: has-output
    entity: network
  - verb: owns
    entity: account
  - verb: has-account
    entity: user
- related:
  - verb: has-output
    entity: network
  - verb: owns
    entity: account
  - verb: has-account
    entity: administrator
references:
- kind: code
  role: implementation
  target: server/db/messages.ts
- kind: code
  role: implementation
  target: server/services/ircConnection.ts
---

# Network log changes require the stated owner or bound entry authority

Owned history, authorized Agent read and supported B playback; changes restricted to own read/clear facts with actual guards.
