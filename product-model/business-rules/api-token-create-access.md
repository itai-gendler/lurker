---
appliesTo:
- type: entity
  id: api-token
  effect: creates
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
  - entity: account
    fact: Pause status
    is: Active
  configuredBy: account
- related:
  - verb: owns
    entity: account
  - verb: has-account
    entity: administrator
  when:
  - entity: instance-settings
    fact: Edition
    is: standalone
  - entity: account
    fact: Pause status
    is: Active
  configuredBy: account
references:
- kind: code
  role: implementation
  target: server/db/apiTokens.ts
- kind: code
  role: implementation
  target: server/routes/apiTokens.ts
- kind: code
  role: implementation
  target: server/middleware/auth.ts#requireAuth
- kind: code
  role: implementation
  target: server/db/accountRecovery.ts
---

# API token creation requires the stated owner or bound entry authority

Owned standalone management, active-account writes and scope checks; revoke changes retained Revocation; unattended last-use update.

The Account-configured management grant selects the actual authenticated ordinary-session or accepted OAuth caller, requires that same owner currently unpaused and applies only to the selected owned token. API-token credentials do not authenticate this ordinary REST management route.
