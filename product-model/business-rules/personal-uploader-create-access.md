---
appliesTo:
- type: entity
  id: personal-uploader
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
  target: server/db/uploaderConfig.ts
- kind: code
  role: implementation
  target: server/routes/uploaders.ts
- kind: code
  role: implementation
  target: server/services/importService.ts
- kind: code
  role: implementation
  target: server/db/exportSchema.ts
---

# Personal uploader creation requires the stated owner or bound entry authority

Only the authenticated unpaused owner creates a destination while personal creation is enabled and the driver is creatable/allowed under effective instance policy.

Eligible archive restoration keeps its separate zero-network, archive-validation and replacement conditions; it does not infer that every restored row passes the interactive add form’s ceremony or creation-policy check.
