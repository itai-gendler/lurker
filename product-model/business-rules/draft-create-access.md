---
appliesTo:
- type: entity
  id: draft
  effect: creates
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

# Draft creation requires the stated owner or bound entry authority

Only the owner saves the selected conversation’s text/reply under its actual local WS or active HTTP flush path. Reply references must be eligible and owned; invalid references are dropped.
