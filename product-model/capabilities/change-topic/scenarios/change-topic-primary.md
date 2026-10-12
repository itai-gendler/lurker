---
kind: primary
routes:
  web: Web
  client: Client API
  irc: IRC bouncer
steps:
- text: The User invokes change topic.
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
- text: If the upstream accepts and reports the result, the Product updates the observed topic.
  kind: product
  entities:
  - entity: channel
    effect: changes
    facts:
    - Topic
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
  target: server/services/verbs/setTopic.ts
- kind: code
  role: implementation
  target: server/services/ircConnection.ts
---

# Change topic

## Trigger

The User invokes change topic.

## Outcome

Topic change requested; upstream result reported

The requested topic is submitted; the upstream governs acceptance and observed topic results.
