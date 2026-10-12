---
kind: exception
routes:
  web: Web
  client: Client API
  irc: IRC bouncer
steps:
- text: The User submits a notice to an encryption-enabled conversation target.
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
- text: No notice is sent. WS can acknowledge manager success and emit an app warning; the bouncer follows
    its explicit refusal contract.
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

# Send message encrypted notice refused

## Trigger

The User submits a notice to an encryption-enabled channel.

## Outcome

No notice is sent. WS can acknowledge manager success and emit an app warning; the bouncer follows its explicit refusal contract.
