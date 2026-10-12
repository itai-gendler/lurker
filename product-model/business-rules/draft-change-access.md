---
appliesTo:
- type: entity
  id: draft
  effect: changes
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

# Draft changes require the stated owner or bound entry authority

Only the owner replaces its draft with the last-write text/reply under the same transport-specific guards. Invalid reply correction retains supported text.
