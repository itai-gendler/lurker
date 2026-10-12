---
kind: path
routes:
  web: Web
  client: Client API
steps:
- text: The User opens a known conversation shell whose history has not yet been hydrated.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::network-log
    client:
      place: client-api::personal
  actor: user
- text: Retained network output hydrates the known shell without a JOIN or reopening. Channel/DM hydration
    uses the same independent history lookup with its own subject facts.
  kind: product
  entities:
  - entity: network-log
    effect: reads
    facts:
    - Entries
    - Read boundary
    - Clear boundary
    - Unread counts
  - entity: channel
    effect: reads
    facts: []
  - entity: network
    effect: reads
    facts: []
  contexts: *id001
  actor: user
references:
- kind: code
  role: implementation
  target: server/db/messages.ts
- kind: code
  role: implementation
  target: server/routes/search.ts
- kind: code
  role: implementation
  target: server/routes/activity.ts
- kind: code
  role: implementation
  target: server/routes/bookmarks.ts
- kind: code
  role: implementation
  target: server/services/wsHub.ts
- kind: code
  role: implementation
  target: server/services/bouncer.ts
- kind: code
  role: implementation
  target: server/services/verbs/recentMessages.ts
- kind: code
  role: implementation
  target: server/services/verbs/searchMessages.ts
- kind: code
  role: implementation
  target: vue_client/src/lib/historyPaging.ts
---

# Browse messages lazy shell

## Trigger

The User opens a known conversation shell whose history has not yet been hydrated.

## Outcome

Retained network output hydrates the known shell without a JOIN or reopening. Channel/DM hydration uses the same independent history lookup with its own subject facts.
