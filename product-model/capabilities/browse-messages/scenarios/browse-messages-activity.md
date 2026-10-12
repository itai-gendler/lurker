---
kind: path
routes:
  web: Web
  client: Client API
steps:
- text: The User opens the retained activity projection with supported filters.
  kind: actor
  entities:
  - entity: message
    effect: reads
    facts: []
  contexts: &id001
    web:
      place: web::personal::activity
    client:
      place: client-api::personal
  actor: user
- text: Supported activity projection returned
  kind: product
  entities:
  - entity: message
    effect: reads
    facts:
    - Sender
    - Content
    - Time
    - Highlight information
    - Reply context
  - entity: reaction
    effect: reads
    facts:
    - Value
    - Reacting identity
    - Self attribution
    - Reacted at
    - Removed at
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

# Browse messages activity

## Trigger

The User opens the retained activity projection with supported filters.

## Outcome

Supported activity projection returned
