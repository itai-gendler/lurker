---
appliesTo:
- type: entity
  id: irc-client
  effect: reads
permits:
- related:
  - verb: owns
    entity: account
  - verb: has-account
    entity: user
  when:
  - entity: instance-settings
    fact: Edition
    is: standalone
- related:
  - verb: owns
    entity: account
  - verb: has-account
    entity: administrator
  when:
  - entity: instance-settings
    fact: Edition
    is: standalone
references:
- kind: code
  role: implementation
  target: server/services/bouncer.ts
---

# IRC client disclosure requires the stated owner or bound entry authority

Supported account credentials, active account, limits and binding; negotiated state/presence; owned or unattended closure.
