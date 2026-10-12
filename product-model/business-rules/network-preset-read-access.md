---
appliesTo:
- type: entity
  id: network-preset
  effect: reads
permits:
- actors:
  - user
  - administrator
references:
- kind: code
  role: implementation
  target: server/routes/adminNetworks.ts
---

# Network preset disclosure requires the stated owner or bound entry authority

Offered information to authenticated users; Admin configuration with actual continuity/validation conditions.
