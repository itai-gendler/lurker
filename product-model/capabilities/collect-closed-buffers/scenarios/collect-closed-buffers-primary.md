---
kind: primary
routes:
  web: Web
  client: Client API
  irc: IRC bouncer
steps:
- text: The closed-subject maintenance schedule examines old closed conversations.
  kind: condition
  entities: []
  contexts: &id001
    web:
      place: web::personal::buffers
    client:
      place: client-api::personal
    irc:
      place: irc-bouncer::personal
  unattended: true
- text: Eligible closed subjects removed unattended
  kind: product
  entities:
  - entity: channel
    effect: removes
    from: Closed
  - entity: direct-message
    effect: removes
    from: Closed
  contexts: *id001
references:
- kind: code
  role: implementation
  target: server/services/retentionSweeper.ts
- kind: code
  role: implementation
  target: server/db/buffers.ts
---

# Collect closed buffers

## Trigger

The closed-subject maintenance schedule examines old closed conversations.

## Outcome

Eligible closed subjects removed unattended

Only otherwise eligible old closed subjects are collected unattended; bookmarks and a reopening guard can preserve them.
