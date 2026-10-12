---
appliesTo:
- type: entity
  id: personal-uploader
  effect: changes
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
---

# Personal uploader changes require the stated owner or bound entry authority

Only the authenticated unpaused owner edits its destination under driver validation. Omitted secret values retain existing credentials; disabling new personal creation does not forbid these edits.
