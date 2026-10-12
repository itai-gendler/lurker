---
appliesTo:
- type: entity
  id: network
  effect: changes
  contexts:
  - place: web::personal
  - place: client-api::personal
  - place: irc-bouncer::personal
  facts:
  - Listed channels
  - Directory progress
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
- unattended: true
references:
- kind: code
  role: implementation
  target: server/db/networks.ts
- kind: code
  role: implementation
  target: server/routes/networks.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
---

# Network changes require the stated owner or bound entry authority

Only the authenticated unpaused owner’s live outbound LIST path refreshes this directory. Cache browsing does not inherit that fresh-query requirement.

Unattended permission is limited to the attributable received event, expiry, delivery-health update or eligible maintenance/parent cleanup described for this operation; it does not authorize arbitrary scheduled account mutation.
