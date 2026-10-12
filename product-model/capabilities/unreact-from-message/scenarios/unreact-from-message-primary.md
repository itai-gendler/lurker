---
kind: primary
routes:
  web: Web
  client: Client API
  irc: IRC bouncer
  web-direct-message: Web direct message
steps:
- text: The User invokes unreact from message.
  kind: actor
  entities:
  - entity: message
    effect: reads
    facts: []
  contexts: &id001
    web:
      place: web::personal::channel
    client:
      place: client-api::personal
    irc:
      place: irc-bouncer::personal
    web-direct-message:
      place: web::personal::direct-message
  actor: user
- text: Eligible reaction withdrawn with tombstone
  kind: product
  entities:
  - entity: reaction
    effect: changes
    facts:
    - Removed at
    to: Withdrawn
    from: Active
  contexts: *id001
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
  target: server/db/reactions.ts
- kind: code
  role: implementation
  target: server/services/bouncer.ts
---

# Unreact from message

## Trigger

The User invokes unreact from message.

## Outcome

Eligible reaction withdrawn with tombstone

Withdrawal retains a MAX-timestamp tombstone rather than deleting independently; stale replay cannot revive it.
