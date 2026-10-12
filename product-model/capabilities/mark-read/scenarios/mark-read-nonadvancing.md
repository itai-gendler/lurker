---
kind: exception
routes:
  web: Web
  client: Client API
  irc: IRC bouncer
  web-direct-message: Web direct message
steps:
- text: The User submits an accepted marker equal to or older than the stored boundary.
  kind: actor
  entities: []
  contexts: &id002
    web:
      place: web::personal::channel
    client:
      place: client-api::personal
    irc:
      place: irc-bouncer::personal
    web-direct-message:
      place: web::personal::direct-message
  actor: user
- text: For the selected supported buffer, the stored pointer does not regress. A bouncer marker query or nonmoving
    update responds only to the requester.
  kind: product
  entities:
  - entity: channel
    effect: reads
    facts: &id001
    - Read boundary
  - entity: direct-message
    effect: reads
    facts: *id001
  contexts: *id002
  actor: user
references:
- kind: code
  role: implementation
  target: server/services/wsHub.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
- kind: code
  role: implementation
  target: server/db/buffers.ts
- kind: code
  role: implementation
  target: vue_client/src/stores/buffers.ts
- kind: code
  role: implementation
  target: server/db/bufferReads.ts
- kind: code
  role: implementation
  target: server/services/bouncer.ts
---

# Mark read nonadvancing

## Trigger

The User submits an accepted marker equal to or older than the stored boundary.

## Outcome

The stored pointer does not regress. A bouncer marker query or nonmoving update responds only to the requester.

Only the addressed channel or private-message marker is read or changed; server/system/DCC targets are excluded by the bouncer contract.
