---
appliesTo:
- type: entity
  id: personal-uploader
  effect: removes
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
---

# Personal uploader removal requires the stated owner or bound entry authority

Only the authenticated unpaused owner removes its destination. A later creation lockdown does not prohibit removal of an existing owned destination.

An eligible authenticated import has a separate account-scoped replacement/failed-insertion cleanup path in importService. It removes the affected retained roots as that import’s replacement or reset requires; upload cleanup removes local history metadata and does not assert provider-byte deletion. This exception requires the current unpaused importing account, zero-network entry guard and the actual validated replacement attempt. It is not a general bypass of interactive deletion guards.
