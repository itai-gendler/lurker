---
appliesTo:
- type: entity
  id: network-certificate
  effect: reads
permits:
- related:
  - verb: uses-certificate
    entity: network
  - verb: owns
    entity: account
  - verb: has-account
    entity: user
- related:
  - verb: uses-certificate
    entity: network
  - verb: owns
    entity: account
  - verb: has-account
    entity: administrator
references:
- kind: code
  role: implementation
  target: server/routes/networks.ts
---

# Network certificate disclosure requires the stated owner or bound entry authority

HTTP Owner and valid supported TLS pair; private credential read only through owned export; replacement removes prior pair.
