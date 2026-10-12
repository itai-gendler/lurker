---
kind: exception
routes:
  web: Web
  client: Client API
steps:
- text: The User resumes a conversation whose supplied slice boundary is no longer contiguous with retained
    history.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::lurker-log
    client:
      place: client-api::personal
  actor: user
- text: A discontinuity replaces the bounded live slice instead of appending an unsafe gap. The networkless
    log uses its own sequence and is replaced rather than merged by IRC message IDs.
  kind: product
  entities:
  - entity: message
    effect: reads
    facts:
    - Sender
    - Content
    - Kind
    - Time
    - Self attribution
    - Upstream identity
    - Reply context
    - Highlight information
    - Ignore information
    - Encryption indication
  - entity: lurker-log
    effect: reads
    facts:
    - Entries
    - Read boundary
    - Unread counts
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

# Browse messages resume gap

## Trigger

The User resumes a conversation whose supplied slice boundary is no longer contiguous with retained history.

## Outcome

A discontinuity replaces the bounded live slice instead of appending an unsafe gap. The networkless log uses its own sequence and is replaced rather than merged by IRC message IDs.
