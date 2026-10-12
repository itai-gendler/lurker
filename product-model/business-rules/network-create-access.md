---
appliesTo:
- type: entity
  id: network
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
  target: server/db/networks.ts
- kind: code
  role: implementation
  target: server/routes/networks.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
---

# Network creation requires the stated owner or bound entry authority

Only the authenticated owner’s active HTTP path creates a valid configuration under effective host/proxy policy. Archive import instead requires a validated archive and zero-network eligibility. Bouncer clients cannot create networks.
