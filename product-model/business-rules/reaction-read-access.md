---
appliesTo:
- type: entity
  id: reaction
  effect: reads
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
- related:
  - verb: has-association
    entity: message
  - verb: contains
    entity: network
  - verb: owns
    entity: account
  - verb: has-account
    entity: administrator
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

# Reaction disclosure requires the stated owner or bound entry authority

Owned/bound upstream-eligible operation or accepted incoming event; withdrawal changes tombstone rather than offering independent deletion.

The selected retained Message belongs directly to its Network, whether its target is a Channel, Direct message or server output. This ownership path does not depend on a Channel relation; reaction authority follows the selected Message into the same owned Network.
