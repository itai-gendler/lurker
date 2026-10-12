---
kind: path
routes:
  web: Web
  client: Client API
  irc: IRC bouncer
  web-direct-message: Web direct message
steps:
- text: The User submits an action through the supported conversation send path.
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
- text: Supported action submitted
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
  target: server/services/verbs/sendMessage.ts
- kind: code
  role: implementation
  target: server/services/verbs/sendAction.ts
- kind: code
  role: implementation
  target: server/services/verbs/sendNotice.ts
- kind: code
  role: implementation
  target: server/services/bouncer.ts
---

# Send message action

## Trigger

The User submits an action through the supported conversation send path.

## Outcome

Supported action submitted
