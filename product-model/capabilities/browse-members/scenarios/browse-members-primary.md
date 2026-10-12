---
kind: primary
routes:
  web: Web
  client: Client API
  irc: IRC bouncer
steps:
- text: The User invokes browse members.
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
- text: Observed channel membership returned
  kind: product
  entities:
  - entity: channel
    effect: reads
    facts:
    - Members
  - entity: irc-user
    effect: reads
    facts:
    - Nick
    - Membership status
    - Presence
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
  target: server/services/verbs/listMembers.ts
---

# Browse members

## Trigger

The User invokes browse members.

## Outcome

Observed channel membership returned

Observed membership is returned; MCP sorts results and reports truncation/total with its default 200 and maximum 1000 result limit.
