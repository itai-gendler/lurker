---
kind: primary
routes:
  web: Web
  client: Client API
  irc: IRC bouncer
steps:
- text: The User invokes change nick.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::channel
    client:
      place: client-api::personal
    irc:
      place: irc-bouncer::personal
  actor: user
- text: The Product submits NICK on the selected live connection.
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
- text: If the upstream accepts and reports a self-nick change, the Product updates the observed identity.
  kind: product
  entities:
  - entity: network
    effect: changes
    facts:
    - Current nick
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
  target: server/services/verbs/setNick.ts
- kind: code
  role: implementation
  target: server/services/ircConnection.ts
---

# Change nick

## Trigger

The User invokes change nick.

## Outcome

Nick change requested; upstream outcome reported where supported

A nick change is requested and observed upstream nick state is updated when reported.

The request acknowledgement does not establish a changed current nick. Preferred nick remains the configured reconnect preference; changing it belongs to network configuration.
