---
kind: primary
routes:
  web: Web
  client: Client API
  irc: IRC bouncer
steps:
- text: The User invokes change channel modes.
  kind: actor
  entities:
  - entity: channel
    effect: reads
    facts: []
  contexts: &id001
    web:
      place: web::personal::channel
    client:
      place: client-api::personal
    irc:
      place: irc-bouncer::personal
  actor: user
- text: The Product submits the requested IRC change on the selected live connection.
  kind: product
  entities:
  - entity: network
    effect: reads
    facts:
    - Connection state
  contexts:
    web:
      place: web::personal::channel
    client:
      place: client-api::personal
    irc:
      place: irc-bouncer::personal
  actor: user
- text: If the upstream accepts and reports the result, the Product updates the observed modes.
  kind: product
  entities:
  - entity: channel
    effect: changes
    facts:
    - Modes
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
  target: server/services/verbs/setChannelModes.ts
- kind: code
  role: implementation
  target: server/services/ircConnection.ts
---

# Change channel modes

## Trigger

The User invokes change channel modes.

## Outcome

Mode changes requested; upstream results reported

Supported mode changes are submitted and subsequent upstream results determine observed modes.
