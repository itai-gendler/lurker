---
appliesTo:
- type: entity
  id: network
  effect: changes
  contexts:
  - place: web::personal
  - place: client-api::personal
  facts:
  - Name
  - Connection configuration
  - Authentication
  - Connection preferences
  - Startup channels
  - Preferred nick
  - Position
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

Only the owner’s supported configuration path changes these saved fields. HTTP writes require an unpaused account; nick/away WS and shared-action paths keep their actual writer guards. Host changes recheck host policy; configuration changes need not reconnect immediately.

Unattended permission is limited to the attributable received event, expiry, delivery-health update or eligible maintenance/parent cleanup described for this operation; it does not authorize arbitrary scheduled account mutation.

Network reorder changes Position under the active authenticated owner’s HTTP write authority. The supplied array length must equal the current network count and each Number-coerced element must be an integer in that owner’s current set. A mismatch returns 409 with the current roster before writes. The implementation does not independently reject duplicates; a duplicate can leave an omitted row’s prior position unchanged. This is not a stronger permutation guarantee.
