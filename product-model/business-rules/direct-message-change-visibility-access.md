---
appliesTo:
- type: entity
  id: direct-message
  effect: changes
  contexts:
  - place: web::personal
  - place: client-api::personal
  facts:
  - Visibility
permits:
- related:
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
  target: server/db/buffers.ts
- kind: code
  role: implementation
  target: server/services/wsHub.ts
---

# Direct message changes require the stated owner or bound entry authority

Owned open/accepted conversation/import; owned reads; local changes and visibility changes keep distinct transport guards; eligible collection/parent removal.

Unattended permission is limited to the attributable received event, expiry, delivery-health update or eligible maintenance/parent cleanup described for this operation; it does not authorize arbitrary scheduled account mutation.
