---
kind: primary
routes:
  web: Web
  client: Client API
  irc: IRC bouncer
steps:
- text: The User invokes part channel.
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
- text: PART requested; autojoin intent lowered
  kind: product
  entities:
  - entity: channel
    effect: changes
    facts:
    - Autojoin
  contexts: *id001
  actor: user
- text: If the upstream reports the completed PART, the Product updates observed membership while retaining the
    conversation.
  kind: product
  entities:
  - entity: channel
    effect: changes
    facts:
    - Joined status
  actor: user
  contexts:
    web:
      place: web::personal::channel
    client:
      place: client-api::personal
    irc:
      place: irc-bouncer::personal
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
  target: server/services/verbs/partChannel.ts
---

# Part channel

## Trigger

The User invokes part channel.

## Outcome

PART requested; autojoin intent lowered

PART lowers join intent while retaining the buffer/history. The bouncer does not establish the comment’s second-PART/Close equivalence.
