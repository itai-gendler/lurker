---
appliesTo:
- type: entity
  id: image-upload
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

# Image upload changes require the stated owner or bound entry authority

Only the authenticated, unpaused owner changes Favorite status on its retained upload history. Upload creation, reading and provider-backed removal have separate grants.
