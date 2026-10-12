---
kind: primary
routes:
  web: Web
  client: Client API
  irc: IRC bouncer
steps:
- text: The User invokes read topic.
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
- text: Current/last-known topic returned; bouncer query follows upstream IRC
  kind: product
  entities:
  - entity: channel
    effect: reads
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
  target: server/services/verbs/getTopic.ts
---

# Read topic

## Trigger

The User invokes read topic.

## Outcome

Current/last-known topic returned; bouncer query follows upstream IRC

Current or last-known topic is returned through the MCP observation tool. A bouncer topic query follows upstream IRC.
