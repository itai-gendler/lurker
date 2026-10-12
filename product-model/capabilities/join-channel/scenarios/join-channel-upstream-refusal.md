---
kind: exception
routes:
  web: Web
  client: Client API
  irc: IRC bouncer
steps:
- text: The User requests a join that the upstream server refuses.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::channel-list
    client:
      place: client-api::personal
    irc:
      place: irc-bouncer::personal
  actor: user
- text: Upstream refusal does not establish confirmed joined state
  kind: product
  entities: []
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
  target: server/services/verbs/joinChannel.ts
- kind: code
  role: implementation
  target: vue_client/src/components/ChannelListModal.vue
---

# Join channel upstream refusal

## Trigger

The User requests a join that the upstream server refuses.

## Outcome

Upstream refusal does not establish confirmed joined state
