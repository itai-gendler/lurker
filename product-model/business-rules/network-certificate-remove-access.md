---
appliesTo:
- type: entity
  id: network-certificate
  effect: removes
permits:
- related:
  - verb: uses-certificate
    entity: network
  - verb: owns
    entity: account
  - verb: has-account
    entity: user
  when:
  - entity: account
    fact: Pause status
    is: Active
- related:
  - verb: uses-certificate
    entity: network
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
  target: server/routes/networks.ts
---

# Network certificate removal requires the stated owner or bound entry authority

HTTP Owner and valid supported TLS pair; private credential read only through owned export; replacement removes prior pair.
