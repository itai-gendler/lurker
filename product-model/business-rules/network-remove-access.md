---
appliesTo:
- type: entity
  id: network
  effect: removes
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
  target: server/db/networks.ts
- kind: code
  role: implementation
  target: server/routes/networks.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
---

# Network removal requires the stated owner or bound entry authority

Create/remove: HTTP Owner active. Read: owned disclosure/Agent read/bound B contract. Configuration: owned actual HTTP/WS guards. Connection: IRC writer/Agent write or attributable unattended events. Directory: fresh-query guard, distinct from cached read. Administrative state: suspension/resume consequences only.
