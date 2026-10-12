---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: "The User clears this nick\u2019s relay attribution mark."
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::profile
    client:
      place: client-api::personal
  actor: user
- text: Mark removed
  kind: product
  entities:
  - entity: relay-bot
    effect: removes
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
  target: server/services/verbs/setRelayBot.ts
---

# Unmark relay bot

## Trigger

The User invokes unmark relay bot.

## Outcome

Mark removed
