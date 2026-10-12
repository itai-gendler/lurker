---
appliesTo:
- type: entity
  id: reaction
  effect: creates
permits:
- related:
  - verb: has-association
    entity: message
  - verb: contains
    entity: network
  - verb: owns
    entity: account
  - verb: has-account
    entity: user
  when:
  - entity: account
    fact: Pause status
    is: Active
- related:
  - verb: has-association
    entity: message
  - verb: contains
    entity: network
  - verb: owns
    entity: account
  - verb: has-account
    entity: administrator
  when:
  - entity: account
    fact: Pause status
    is: Active
- unattended: true
references:
- kind: code
  role: implementation
  target: server/db/reactions.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
- kind: code
  role: implementation
  target: server/db/index.ts
- kind: code
  role: implementation
  target: server/db/messages.ts
---

# Reaction creation requires the stated owner or bound entry authority

Owned/bound upstream-eligible operation or accepted incoming event; withdrawal changes tombstone rather than offering independent deletion.

Unattended permission is limited to the attributable received event, expiry, delivery-health update or eligible maintenance/parent cleanup described for this operation; it does not authorize arbitrary scheduled account mutation.

The selected retained Message belongs directly to its Network, whether its target is a Channel, Direct message or server output. This ownership path does not depend on a Channel relation; reaction authority follows the selected Message into the same owned Network.
