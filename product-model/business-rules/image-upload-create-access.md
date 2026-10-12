---
appliesTo:
- type: entity
  id: image-upload
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

# Image upload creation requires the stated owner or bound entry authority

Accepted authenticated upload; owned history versus public key-addressed bytes; owned favorite changes; owned nonremoved deletable row after successful provider deletion.

Eligible archive restoration keeps its separate zero-network, archive-validation and replacement conditions; it does not infer that every restored row passes the interactive add form’s ceremony or creation-policy check.
