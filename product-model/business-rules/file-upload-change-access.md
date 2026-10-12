---
appliesTo:
- type: entity
  id: file-upload
  effect: changes
  facts:
  - Favorite status
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
---

# File upload changes require the stated owner or bound entry authority

Same operation boundaries, excluding image-only facts.
