---
appliesTo:
- type: entity
  id: network-certificate
  effect: creates
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
- kind: code
  role: implementation
  target: server/services/importService.ts
- kind: code
  role: implementation
  target: server/db/exportSchema.ts
---

# Network certificate creation requires the stated owner or bound entry authority

HTTP Owner and valid supported TLS pair; private credential read only through owned export; replacement removes prior pair.

Eligible archive restoration keeps its separate zero-network, archive-validation and replacement conditions; it does not infer that every restored row passes the interactive add form’s ceremony or creation-policy check.
