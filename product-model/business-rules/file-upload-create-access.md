---
appliesTo:
- type: entity
  id: file-upload
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
  target: server/db/uploadHistory.ts
- kind: code
  role: implementation
  target: server/services/uploadService.ts
- kind: code
  role: implementation
  target: server/services/importService.ts
- kind: code
  role: implementation
  target: server/db/exportSchema.ts
---

# File upload creation requires the stated owner or bound entry authority

Same operation boundaries, excluding image-only facts.

Eligible archive restoration keeps its separate zero-network, archive-validation and replacement conditions; it does not infer that every restored row passes the interactive add form’s ceremony or creation-policy check.
