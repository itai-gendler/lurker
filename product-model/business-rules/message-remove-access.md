---
appliesTo:
- type: entity
  id: message
  effect: removes
permits:
- related:
  - verb: contains
    entity: network
  - verb: owns
    entity: account
  - verb: has-account
    entity: user
- related:
  - verb: contains
    entity: network
  - verb: owns
    entity: account
  - verb: has-account
    entity: administrator
- unattended: true
references:
- kind: code
  role: implementation
  target: server/db/messages.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
- kind: code
  role: implementation
  target: server/db/index.ts
---

# Message removal requires the stated owner or bound entry authority

Only eligible unattended retention/parent cleanup removes retained content, or the authorized owner/admin removes the containing network/account. Bookmarks, bounded reply context and import/export deferral constrain pruning.

Unattended permission is limited to the attributable received event, expiry, delivery-health update or eligible maintenance/parent cleanup described for this operation; it does not authorize arbitrary scheduled account mutation.

The selected retained Message belongs directly to its Network, whether its target is a Channel, Direct message or server output. The same account and matched-credential restrictions apply to every such target.
