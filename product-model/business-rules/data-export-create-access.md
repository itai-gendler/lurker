---
appliesTo:
- type: entity
  id: data-export
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
  target: server/services/exportJobs.ts
- kind: code
  role: implementation
  target: server/routes/exports.ts
---

# Data export creation requires the stated owner or bound entry authority

Only the authenticated unpaused HTTP owner starts/reuses its archive job under selection and one-in-flight limits. A paused POST is refused despite contrary older documentation.
