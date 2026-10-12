---
appliesTo:
- type: entity
  id: draft
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
  target: server/db/drafts.ts
- kind: code
  role: implementation
  target: server/routes/drafts.ts
---

# Draft disclosure requires the stated owner or bound entry authority

Owner; local WS save/clear versus active HTTP flush; invalid reply correction; parent cleanup.
