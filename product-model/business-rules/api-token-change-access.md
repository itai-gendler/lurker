---
appliesTo:
- type: entity
  id: api-token
  effect: changes
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
- actors:
  - user
  - administrator
  configuredBy: recovery-link
  when:
  - entity: instance-settings
    fact: Edition
    is: standalone
- unattended: true
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
- kind: code
  role: implementation
  target: server/middleware/auth.ts#requireAuth
- kind: code
  role: implementation
  target: server/db/accountRecovery.ts
---

# API token changes require the stated owner or bound entry authority

Owned standalone management, active-account writes and scope checks; revoke changes retained Revocation; unattended last-use update.

Unattended permission is limited to the attributable received event, expiry, delivery-health update or eligible maintenance/parent cleanup described for this operation; it does not authorize arbitrary scheduled account mutation.

Valid presented recovery proof selects its exact target account and revokes that account’s active tokens as credential replacement completes, even when that target is paused. This exception changes Revocation only and grants no token creation or scope editing authority.

The Account-configured management grant selects the actual authenticated ordinary-session or accepted OAuth caller, requires that same owner currently unpaused and applies only to the selected owned token. API-token credentials do not authenticate this ordinary REST management route.
