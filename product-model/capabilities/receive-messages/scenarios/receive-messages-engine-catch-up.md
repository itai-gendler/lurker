---
kind: path
routes:
  web: Web
  client: Client API
  irc: IRC bouncer
steps:
- text: Incoming IRC activity or available engine backlog arrives.
  kind: condition
  entities: []
  contexts: &id001
    web:
      place: web::personal::channel
    client:
      place: client-api::personal
    irc:
      place: irc-bouncer::personal
  unattended: true
- text: Available engine backlog is reconciled, using upstream identity or the catch-up content/time fallback.
    This does not imply a second IRC-state writer.
  kind: product
  entities:
  - entity: message
    effect: creates
    facts:
    - Sender
    - Content
    - Kind
    - Time
    - Self attribution
    - Upstream identity
    - Reply context
    - Highlight information
    - Ignore information
    - Encryption indication
    to: Recorded
  contexts: *id001
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
  target: server/services/ircConnection.ts
- kind: code
  role: implementation
  target: server/services/bouncer.ts
---

# Receive messages engine catch up

## Trigger

The Product adopts a held upstream connection with available engine backlog.

## Outcome

Available engine backlog is reconciled, using upstream identity or the catch-up content/time fallback. This does not imply a second IRC-state writer.
