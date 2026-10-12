---
appliesTo:
- type: entity
  id: api-token
  effect: reads
permits:
- related:
  - verb: owns
    entity: account
  - verb: has-account
    entity: user
  when:
  - entity: instance-settings
    fact: Edition
    is: standalone
- related:
  - verb: owns
    entity: account
  - verb: has-account
    entity: administrator
  when:
  - entity: instance-settings
    fact: Edition
    is: standalone
references:
- kind: code
  role: implementation
  target: server/db/apiTokens.ts
- kind: code
  role: implementation
  target: server/routes/apiTokens.ts
---

# API token disclosure requires the stated owner or bound entry authority

Owned standalone management, active-account writes and scope checks; revoke changes retained Revocation; unattended last-use update.
