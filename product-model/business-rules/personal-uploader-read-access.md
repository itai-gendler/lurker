---
appliesTo:
- type: entity
  id: personal-uploader
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
  target: server/db/uploaderConfig.ts
- kind: code
  role: implementation
  target: server/routes/uploaders.ts
---

# Personal uploader disclosure requires the stated owner or bound entry authority

HTTP Owner; creation additionally requires allowed personal creation/creatable driver. Creation lockdown does not forbid existing-row edit/removal.
